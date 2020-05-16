---
layout: post
title: 题解们
permalink: /solutions.html
---

* auto-gen TOC:
{:toc}
## 前言

好懒哦，为什么要写题解

------

代码贴多了Typora会变卡~



## 数论

### 卡特兰数

[Gym102501J](/post/solutions/Gym102501.html)




## 数据结构
### Splay
[POJ-3468](/post/solutions/POJ3468.html)
一道典型的线段树题，于是就用Splay做了



#### [BZOJ 1251](http://www.lydsy.com/JudgeOnline/problem.php?id=1251)

套splay模板即可，注意pushup时检查子节点是否存在(就因为这个WA了4发)

```c++
#include <bits/stdc++.h>
#define ll long long
#define Android ios::sync_with_stdio(false), cin.tie(NULL)

using namespace std;

const int maxn=6e4+500;
 
int child[maxn][2], par[maxn], sz[maxn]={0}, tag[maxn]={0};
ll lazy[maxn]={0}, mx[maxn]={0}, val[maxn];
int root, nrof_node = 0;
 
inline void push_up(int rt){
    if(!rt) return;
    sz[rt] = sz[child[rt][0]] + sz[child[rt][1]] + 1;
    mx[rt] = val[rt];
    if(child[rt][0]) mx[rt] = max(mx[rt], mx[child[rt][0]]);
    if(child[rt][1]) mx[rt] = max(mx[rt], mx[child[rt][1]]);
}
 
inline void add(int rt, ll delta){
    if(!rt) return;
    lazy[rt] += delta;
    val[rt] += delta;
    mx[rt] += delta;
}
 
inline void push_down(int rt){
    if(lazy[rt]){
        add(child[rt][0], lazy[rt]);
        add(child[rt][1], lazy[rt]);
        lazy[rt] = 0;
    }
    if(tag[rt]){
        tag[child[rt][0]] ^= 1;
        tag[child[rt][1]] ^= 1;
        swap(child[rt][0], child[rt][1]);
        tag[rt] = 0;
    }
}
 
int build_tree(int l, int r, int p){
    if(l > r) return 0;
    int idx = ++nrof_node;
    int mid = (l + r)>>1;
    val[idx] = 0, par[idx] = p, mx[idx] = 0, tag[idx] = 0;
    child[idx][0] = build_tree(l, mid-1, idx);
    child[idx][1] = build_tree(mid+1, r, idx);
    push_up(idx);
    return idx;
}
 
inline int chk(int rt){
    return child[par[rt]][1] == rt;
}
 
void rotate(int rt){
    int p = par[rt], g = par[p];
    int k = chk(rt), op = child[rt][k^1];
    child[g][chk(p)] = rt, par[rt] = g;
    child[p][k] = op, par[op] = p;
    child[rt][k^1] = p, par[p] = rt;
    push_up(p); push_up(rt);
}
 
void splay(int rt, int goal = 0){
    while(par[rt] != goal){
        if(par[par[rt]] != goal){
            if(chk(rt) == chk(par[rt])) rotate(par[rt]);
            else rotate(rt);
        }
        rotate(rt);
    }
    if(!goal) root = rt;
}
 
int find(int pos){
    int cur = root;
    while(cur){
        push_down(cur);
        if(sz[child[cur][0]] >= pos){
            cur = child[cur][0];
        }else if(sz[child[cur][0]] + 1 >= pos){
            return cur;
        }else{
            pos -= sz[child[cur][0]] + 1;
            cur = child[cur][1];
        }
    }
    return -1;
}
 
void interval_add(int l, int r, ll delta){
    r += 2;
    l = find(l), r = find(r);
    splay(l, 0), splay(r, l);
    add(child[r][0], delta);
}
 
ll interval_query(int l, int r){
    r += 2;
    l = find(l), r = find(r);
    splay(l, 0), splay(r, l);
    return mx[child[r][0]];
}
 
void reverse(int l, int r){
    r += 2;
    l = find(l), r = find(r);
    splay(l, 0), splay(r, l);
    tag[child[r][0]] ^= 1;
}
 
void solve(){
    int n, m;
    cin >> n >> m;
    root = build_tree(0, n+1, 0);
    int op, x, y, k;
    for(int i=0;i<m;i++){
        cin >> op;
        if(op == 1){
            cin >> x >> y >> k;
            interval_add(x, y, k);
        }else{
            cin >> x >> y;
            if(op == 3){
                cout << interval_query(x, y) << '\n';
            }else{
                reverse(x, y);
            }
        }
    }
 
}
 
int main(){
    Android;
    solve();
}

```



## 图论
### 判环
#### [HDU-6736 Forest Program](/post/Graph/HDU6736.html)
$ans = 2^{e_0} * \prod (2^{e_i} - 1)$
其中$e_0$ 为不在环中的边数，$e_i$为各个环中的边数



## 字符串

### 后缀数组

#### UVA760

用的是清华的模板

```c++
#include <bits/stdc++.h>
#define ll long long
#define ull unsigned long long
#define Android ios::sync_with_stdio(false), cin.tie(NULL)
#define F(i, n) for(int i=0, _iter_max=(n); i<_iter_max; i++)
#define range(i, l, r) for(int i=(l), _iter_max=(r); i<_iter_max; i++)

using namespace std;

struct suffix_array{
    const static int N = 620 * 2;
    int n,rank[N],sa[N],height[N],tmp[N],cnt[N];
    char s[N];
    void suffixArray(int n, int m){
        int i, j, k; n++;
        for(i=0; i<n*2+5; i++) rank[i]=sa[i]=height[i]=tmp[i]=0;
        for(i=0;i<m;i++) cnt[i]=0;
        for(i=0;i<n;i++) cnt[rank[i]=s[i]]++; // 预处理需要在外面进行
        for(i=1;i<m;i++) cnt[i]+=cnt[i-1];
        for(i=0;i<n;i++) sa[--cnt[rank[i]]]=i;
        for(k=1;k<=n;k<<=1){
            for(i=0;i<n;i++){
                j = sa[i] - k;
                if(j<0) j+=n;
                tmp[cnt[rank[j]]++] = j;
            }
            sa[tmp[cnt[0]=0]]=j=0;
            for(i=1;i<n;i++){
                if(rank[tmp[i]]!=rank[tmp[i-1]] || 
                rank[tmp[i]+k] != rank[tmp[i-1]+k]) cnt[++j]=i;
                // 在此处统计cnt前缀和
                sa[tmp[i]] = j; // 相当于rank[sa[i]] = j;
            }
            memcpy(rank, sa, n*sizeof(int));
            memcpy(sa, tmp, n*sizeof(int));
            if(j>=n-1) break;
        }
        for(j=rank[height[i=k=0]=0];i<n-1;i++,k++)
            while(~k&&s[i]!=s[sa[j-1]+k]) height[j]=k--, j=rank[sa[j]+1];
    }
}SA; // 模板

void solve(){
    int first = strlen(SA.s);
    SA.s[first] = 'z';
    cin >> (SA.s + first + 1);
    int total = strlen(SA.s);
    F(i, total) SA.s[i] -= 'a' - 1;
    SA.suffixArray(total, 50);
    int len = 0;
    for(int i=2; i<=total; i++){
        int a = SA.sa[i], b = SA.sa[i-1];
        if(a > b) swap(a, b);
        if(a < first && b > first)
            len = max(len, SA.height[i]);
    }
    vector<int> ans; 
    for(int i=2; i<=total; i++){
        if(SA.height[i] < len) continue;
        int j, k, a, b;
        // 相同的后缀只能出现一次
        for(j=i; j<=total && SA.height[j] >= len; j++);
        for(k=i; k<j; k++){
            a = SA.sa[k], b = SA.sa[k-1];
            if(a > b) swap(a, b);
            if(a < first && b > first) break;
        }
        if(k != j) ans.push_back(SA.sa[k]);
        i = j-1;
    }
    if(len == 0){
        cout << "No common sequence.\n";
    }else{
        for(int p:ans){
            for(int i=0;i<len; i++) cout << (char)(SA.s[p+i]+'a'-1);
            cout << '\n';
        }
    }
}

signed main() {
    Android;
    bool first_case = true;
    while(cin >> SA.s) {
        if(!first_case) cout << "\n";
        first_case = false;
        solve();
    }
}
```

这套板子有点怪，等我搞清楚原理再来写题解



#### POJ3693

题解见代码注释

参考题解: https://www.cnblogs.com/kuangbin/archive/2013/04/24/3041323.html 

```c++
#include <set>
#include <cstdio>
#include <iostream>
#include <cmath>
#include <cstring>
#define Android ios::sync_with_stdio(false), cin.tie(NULL)


using namespace std;

const int N = 1e5 + 1e4;
struct suffix_array{ // 后缀数组模板
    int n,rank[N*2],sa[N*2],height[N*2],tmp[N*2],cnt[N*2];
    char s[N];
    void suffixArray(int n, int m){
        int i, j, k; n++;
        for(i=0; i<n*2+5; i++) rank[i]=sa[i]=height[i]=tmp[i]=0;
        for(i=0;i<m;i++) cnt[i]=0;
        for(i=0;i<n;i++) cnt[rank[i]=s[i]]++; // 预处理需要在外面进行
        for(i=1;i<m;i++) cnt[i]+=cnt[i-1];
        for(i=0;i<n;i++) sa[--cnt[rank[i]]]=i;
        for(k=1;k<=n;k<<=1){
            for(i=0;i<n;i++){
                j = sa[i] - k;
                if(j<0) j+=n;
                tmp[cnt[rank[j]]++] = j;
            }
            sa[tmp[cnt[0]=0]]=j=0;
            for(i=1;i<n;i++){
                if(rank[tmp[i]]!=rank[tmp[i-1]] || 
                rank[tmp[i]+k] != rank[tmp[i-1]+k]) cnt[++j]=i;
                sa[tmp[i]] = j; // 相当于rank[sa[i]] = j;
            }
            memcpy(rank, sa, n*sizeof(int));
            memcpy(sa, tmp, n*sizeof(int));
            if(j>=n-1) break;
        }
        for(j=rank[height[i=k=0]=0];i<n-1;i++,k++)
            while(~k&&s[i]!=s[sa[j-1]+k]) height[j]=k--, j=rank[sa[j]+1];
    }
}SA; // 模板

struct RMQ{
    int best[20][N], n;
    void build(int nx){
        n = nx;
        // 不需要特别处理best[0][1]
        for(int i=2; i<=n; i++) best[0][i] = SA.height[i];
        for(int step=1; (1<<step)<=n; step++){
            for(int i=1; i+(1<<step)-1<=n; i++)
                best[step][i] = min(best[step-1][i], best[step-1][i+(1<<(step-1))]);
        }
    }
    int query(int a, int b){
        a = SA.rank[a], b = SA.rank[b];
        if(a > b) swap(a, b);
        a += 1; // [best[x][1] for x in range(0, inf)]永远不会被访问
        int p = log2(b - a + 1);
        return min(best[p][a], best[p][b-(1<<p)+1]);
    }
}rmq;

void solve(){
    int len = strlen(SA.s);
    SA.suffixArray(len, 128);
    rmq.build(len);
    int ans = 0; 
    set<int> idx;
    for(int i=1; i<len; i++){ // i代表循环节长度
        for(int s=0; s+i<len; s+=i){ 
            int com = rmq.query(s, s+i);
            int k = com / i + 1, ak=0;
            // 假设 rmq%i > 0,我们可以试着向左拓展exp=(i-rmq%i)个字符
            // 可知 exp<i, 因此若拓展后使得子串对应的循环次数增加delta,则 delta<=1
            // 同时，若str[s, s+com] == str[s+i, s+i+com]
            // 且 str[s-exp, s+com] != str[s+i-exp, s+i+com]
            // 则定有|lcp(str[s-exp, s+com], str[s+i-exp, s+i+com])| < exp (lcp:最长公共前缀)
            // PS.还不如把字符串反过来再求一遍SA数组......
            int opt = s - (i - com % i);
            if(opt >= 0 && (com % i)>0){
                ak = rmq.query(opt, opt+i)/i+1;
                if(ak > ans) ans = ak, idx.clear();
                if(ak == ans) idx.insert(i);
                // 这里若rmq.query(opt, opt+i) >= com 即可判定循环节数量+1
                // 因为rmq.query(opt, opt+i)要么小于exp,要么大于com
            }
            if(k > ans) ans = k, idx.clear();
            if(k == ans) idx.insert(i);
        }
    }
    // 为什么不能再上面就统计答案不能保证字典序最小？
    // 给出样例:aabcabcabcabcabca
    // 即向左拓展时并不能保证字典序最小
    int from, le=-1;
    for(int i=1; i<=len&&le==-1; i++){ // 遍历sa,保证字典序最小
        for(set<int>::iterator iter = idx.begin(); iter != idx.end(); iter++){
            int l = *iter;
            if(SA.sa[i] + ans * l > len) continue;
            if(rmq.query(SA.sa[i], SA.sa[i] + l) >= (ans-1)*l){
                from = SA.sa[i]; le = l;
                break;
            }
        }
    }
    for(int i=0; i<ans * le; i++) cout << SA.s[i + from];
    cout <<'\n';
}

signed main() {
    Android;
    int c = 1;
    while(cin >> SA.s) {
        if(SA.s[0]=='#') break;
        cout << "Case " << (c++) << ": ";
        solve();
    }
}

```



### 回文树

简单实用的数据结构

#### HDU 6599

```c++
#include <bits/stdc++.h>
#define ll long long
#define Android ios::sync_with_stdio(false), cin.tie(NULL)

using namespace std;

const int N = 3e5 + 1000;
int pos[N];
struct pam{
    const static int S = 26;
    int len[N], child[N][S], fail[N], text[N];
    int last, slen, node_cnt;
    ll cnt[N];

    int new_node(int l){
        for(int i=0; i<S; i++) child[node_cnt][i] = 0;
        len[node_cnt] = l, cnt[node_cnt]=0;
        return node_cnt++;
    }

    void init(){
        slen = node_cnt = last = 0;
        fail[new_node(0)] = 1;
        new_node(-1);
        text[0] = -1;
    }

    int getfail(int x){
        while(text[slen-len[x]-1] != text[slen]) x=fail[x];
        return x;
    }

    void add(int w){
        text[++slen] = w;
        int x = getfail(last);
        if(!child[x][w]){
            int y = new_node(len[x] + 2);
            fail[y] = child[getfail(fail[x])][w];
            child[x][w] = y;
        }
        cnt[last = child[x][w]]++;
        pos[last] = slen;
    }

    void count(){
        for(int i=node_cnt-1; i>0; i--) cnt[fail[i]] += cnt[i];
    }
}pt; // 模板

unsigned ll hsh[N], base = 131;
unsigned ll bs[N];
ll ans[N];
char buffer[N];
unsigned ll get_hash(int l, int r){
    return hsh[r] - hsh[l-1] * bs[r - l + 1];
}

bool check(int p, int l){ // 使用hash判断
    if(l % 2 == 0)
        return get_hash(p-l+1, p-l/2) == get_hash(p-l/2+1, p);
    return get_hash(p-l+1, p-l/2)==get_hash(p-l/2, p);
}

void solve(){
    pt.init();
    int len = strlen(buffer + 1);
    for(int i=0; i<=len; i++) ans[i] = 0;
    for(int i=1; i<=len; i++) hsh[i] = hsh[i-1] * base + buffer[i];
    for(int i=1; i<=len; i++) pt.add(buffer[i]-'a');
    pt.count();
    for(int i=pt.node_cnt-1; i>1; i--){ // 遍历每一种回文子串
        int p = pos[i], le = pt.len[i];
        if(check(p, le)) ans[le] += pt.cnt[i]; // 条件满足即加入答案中
    }
    
    for(int i=1; i<=pt.slen; i++){
        cout << ans[i] << (i==pt.slen?'\n':' ');
    }
}

signed main() {
    Android;
    bs[0] = 1, hsh[0] = 0;
    for(int i=1; i<N; i++) bs[i] = bs[i-1] * base;
    while(cin >> (buffer + 1)) solve();
}
```



## DP

### 决策单调性

#### Codeforces 868F

详见[我的补题列表](/2020/02/22/训练补题.html)



##  代码技巧

### Codechef ANUGCD

详见[我的补题列表](/2020/02/22/训练补题.html)

顺便用上CodeChef SUBLCM里学来的小技巧

```c++
#include <bits/stdc++.h>

using namespace std;

const int inf = 0x3f3f3f3f;
const int maxn = 1e5 + 100;

bool not_prime[maxn] = {0};
vector<int> prime;
int factor[maxn], n, m;

void init(){ // 线性筛
    for(int i=2; i<maxn; i++){
        if(!not_prime[i]) prime.push_back(i), factor[i] = i;
        for(int j=0; j<prime.size() && i*prime[j] < maxn; j++){
            not_prime[i*prime[j]] = true;
            factor[i*prime[j]] = prime[j];
            if(i % prime[j] == 0) break;
        }
    }
}

vector<int> bit[maxn], pos[maxn], val[maxn], cnt[maxn];

void update(vector<int> & bit, int value, int pos){
    for(int i=pos; i<bit.size(); i+=(-i)&i){
        bit[i] = max(bit[i], value);
    }
}

int query(vector<int> & bit, vector<int> & val, int l, int r){
    int ret = val[r], tmp;
    while(l < r){
        tmp = r - ((-r) & r);
        if(tmp >= l){
            ret = max(ret, bit[r]);
            r = tmp;
        }else{
            ret = max(ret, val[r--]);
        }
    }
    return ret;
}

int main(){
	cin >> n >> m;
    for(int i=1, tmp, cur, f; i<=n; i++){
        cin >> tmp;
        cur = tmp;
        cnt[tmp].push_back(i);
        while(cur > 1){ // 由于要求gcd(G,a[i])>1，不需要处理因子1
            f = factor[cur];
            while(cur % f == 0) cur /= f;
            if(val[f].empty()){ // 树状数组从1开始
                val[f].push_back(-1);
                pos[f].push_back(-1);
            }
            val[f].push_back(tmp);
            pos[f].push_back(i);
        }
    }
    for(int i=2; i<maxn; i++){
        if(!val[i].empty()){
            bit[i].resize(val[i].size(), 0);
            for(int j=1; j<val[i].size(); j++){
                update(bit[i], val[i][j], j);
            }
        }
    }
    for(int i=0, g, l, r, f; i<m; i++){
        cin >> g >> l >> r;
        int mx = -1, ccnt = -1;
        while(g > 1){
            f = factor[g];
            while(g % f == 0) g/= f;
            if(bit[f].empty()) continue;
            int low = lower_bound(pos[f].begin(), pos[f].end(), l) - pos[f].begin();
            int high = upper_bound(pos[f].begin(), pos[f].end(), r) - pos[f].begin() - 1;
            if(low <= high) mx = max(mx, query(bit[f], val[f], low-1, high));
        }
        if(mx != -1){
            ccnt = upper_bound(cnt[mx].begin(), cnt[mx].end(), r) -
                   lower_bound(cnt[mx].begin(), cnt[mx].end(), l);
        }
        cout << mx << " " << ccnt << '\n';
    }
}
```



## 其他

### [Codeforces 578D](/post/solutions/Codeforces578D.html)

### [Gym102433G](/post/solutions/Gym102433G.html)

