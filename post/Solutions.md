---
layout: post
title: 题解们
permalink: /solutions.html
---

* auto-gen TOC:
{:toc}
## 说明

本人很懒

## 数据结构
### Splay
#### [POJ-3468](/post/Splay/POJ3468.html)
一道典型的线段树题，于是就用Splay做了



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
            // 则定有lcp(str[s-exp, s+com], str[s+i-exp, s+i+com]) < exp (lcp:最长公共前缀)
            // PS.还不如把字符串反过来再求一遍SA数组......
            int opt = s - (i - com % i);
            if(opt >= 0 && (com % i)>0){
                ak = rmq.query(opt, opt+i)/i+1;
                if(ak > ans) ans = ak, idx.clear();
                if(ak == ans) idx.insert(i);
                // 这里若rmq.query(opt, opt+1) >= com 即可判定循环节数量+1
                // 因为rmq.query(opt, opt+1)要么小于exp,要么大于com
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

```

```