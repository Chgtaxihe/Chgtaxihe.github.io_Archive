---
layout: hidden_page
title: AC自动机学习笔记
---

* auto-gen TOC:
{:toc}
# 前言

![81Ai9A.png](https://s1.ax1x.com/2020/03/15/81Ai9A.png)



# AC自动机

建一个AC自动机分为两步

## 1. 建立一棵Trie树

没有什么要注意的地方。



## 2. 计算fail指针

$fail$指针指向的是后缀相同的串，用一张图来更好地了解fail指针的含义

以下截图来自[参考资料](#参考资料)(1)

![](https://blog.chgtaxihe.top/resource/img/post/ac_automaton_2.PNG)



![](https://blog.chgtaxihe.top/resource/img/post/ac_automaton_1.PNG)



```c++
void calc_fail(){
    queue<int> que;
    for(int i=0;i<26;i++) if(child[0][i]) que.push(child[0][i]);

    while(!que.empty()){
        int p = que.front(); que.pop();

        for(int i=0;i<26;i++){
            if(child[p][i]){
                fail[child[p][i]] = child[fail[p]][i];
                que.push(child[p][i]);
            }else{
                child[p][i] = child[fail[p]][i]; //路径压缩
            }
        }
    }
}
```

我们定义根节点为$0$号节点，当新建节点$u$时，$child[u][i]$初始化为$0$（指向根节点）

将子节点依次入队，是为了避免子节点的$fail$指针指向自己

采用$bfs$，当遍历到节点$v$时， 保证深度小于$dep(v)$的节点的$fail$指针已经计算完毕

$fail[child[p][i]] = child[fail[p]][i];$相当于在当前串$p$与$fail[p]$后都有一个字符$i$，当前串匹配失败，则跳转到共同最长后缀处

路径压缩后就避免了$child[fail[k]][i]$不存在，要继续跳$fail[fail[k]]$的情况



## 匹配

见模板的`count`函数



# 模板

对应题目 [洛谷P3808](https://www.luogu.com.cn/problem/P3808)

```c++
#include <bits/stdc++.h>
#define ll long long
using namespace std;

const int inf = 0x3f3f3f3f;

const int maxn = 1e6 + 1000;
int child[maxn][26], val[maxn], fail[maxn], cnt;

typedef struct Aho_Corasick_Automaton{
    
    Aho_Corasick_Automaton(){
        memset(child, 0, sizeof child);
        memset(val, 0, sizeof val);
        memset(fail, 0, sizeof fail);
        cnt = 1;
    }

    void insert(string s){
        int p = 0, len = s.size();
        for(int i=0;i<len;i++){
            int v = s[i] - 'a';
            if(child[p][v] == 0) child[p][v] = cnt++;
            p = child[p][v];
        }
        val[p]++;
    }

    void calc_fail(){
        queue<int> que;
        for(int i=0;i<26;i++) if(child[0][i]) que.push(child[0][i]);

        while(!que.empty()){
            int p = que.front(); que.pop();

            for(int i=0;i<26;i++){
                if(child[p][i]){
                    fail[child[p][i]] = child[fail[p]][i];
                    que.push(child[p][i]);
                }else{
                    //路径压缩
                    child[p][i] = child[fail[p]][i];
                }
            }
        }
    }

    int count(string s){
        int len = s.size();
        int p = 0, ans = 0;
        for(int i=0;i<len;i++){
            int v = s[i] - 'a';
            p = child[p][v];
            for(int j=p; j && val[j]!=-1; j=fail[j]){ // 沿fail一直往上跳
                ans += val[j];
                //打上标记，避免重复统计
                val[j] = -1;
            }
        }
        return ans;
    }

}ac;

void solve() {
    int n;
    ac tree;
    string buffer;
    cin >> n;
    for(int i=0;i<n;i++){
        cin >> buffer;
        tree.insert(buffer);
    }
    tree.calc_fail();
    cin >> buffer;
    cout << tree.count(buffer) << '\n';
}

signed main() {
    solve();
}
```



# 例题 POJ 2778

对模式串建AC自动机，在trie树上建图，点分为"危险点"和"正常点"，且"危险点"与"正常点"之间没有路。

```c++
#include <cstdio>
#include <cstring>
#define ll long long

using namespace std;

const int maxn = 105;
const int mod = 100000;
int child[maxn][5]={0}, fail[maxn]={0}, danger[maxn]={0}, cnt = 1;
int queue[2 * maxn], head=0, tail=-1;

struct mat{
    ll x[101][101], n;
    void init(int k){
        n = k;
        for(int i=0; i<n; i++) 
            for(int j=0; j<n; j++)
                x[i][j] = 0;
    }

    mat operator *(mat other){
        mat ret; ret.init(n);
        for(int i=0; i<n; i++){
            for(int j=0; j<n; j++){
                for(int k=0; k<n; k++){
                    ret.x[i][j] += x[i][k] * other.x[k][j];
                }
                ret.x[i][j] %= mod;
            }
        }
        return ret;
    }
};

int index(char c){
    if(c == 'A') return 0;
    if(c == 'C') return 1;
    if(c == 'G') return 2;
    if(c == 'T') return 3;
    return 4;
}

struct Aho_Corasick_Automaton{

    void insert(char * str){
        int p = 0, len = strlen(str);
        for(int i=0;i<len;i++){
            int v = index(str[i]);
            if(child[p][v] == 0) child[p][v] = cnt++;
            p = child[p][v];
        }
        danger[p]=1;
    }

    void calc_fail(){
        for(int i=0;i<4;i++) if(child[0][i]) queue[++tail]=child[0][i];
        while(head <= tail){
            int p = queue[head++];
            for(int i=0;i<4;i++){
                if(child[p][i]){
                    fail[child[p][i]] = child[fail[p]][i];
                    queue[++tail] = child[p][i];
                }else{
                    child[p][i] = child[fail[p]][i];
                }
                danger[child[p][i]] |= danger[child[fail[p]][i]]; // 如果child[fail[p]][i]危险，那么child[p][i]也危险
            }
        }
    }

}ac;

ll n, m;

mat qpow(mat base, ll t){
    mat result; result.init(cnt);
    for(int i=0; i<cnt; i++) result.x[i][i] = 1;
    while(t>0){
        if(t & 1) result = result * base;
        t >>= 1;
        base = base * base;
    }
    return result;
}

char buffer[50];

void solve(){
    scanf("%lld%lld", &m, &n);
    for(int i=0; i<m; i++){
        scanf("%s", buffer);
        ac.insert(buffer);
    }
    ac.calc_fail();
    mat base; base.init(cnt);
    for(int i=0; i<cnt; i++){
        if(danger[i]) continue;
        for(int j=0; j<4; j++){
            if(danger[child[i][j]]) continue;
            base.x[i][child[i][j]]++;
        }
    }
    mat result = qpow(base, n);
    ll sum = 0;
    for(int i=0; i<cnt; i++) sum = (sum + result.x[0][i]) % mod;
    cout << sum << endl;
}

signed main(){
    solve();
}
```



# 例题 洛谷P5231

对密码建AC自动机，跑一遍母串，并把沿途所有点（和沿着fail跳转的所有点）都标记一下。最后，对每一个密码，从tire树底部往根部跑，找第一个被标记的点。

```c++
#include <bits/stdc++.h>

using namespace std;

const int maxn = 6e6 + 1000;
const int maxm = 1e5 + 1000;

int tail[maxm], slen[maxm], tcnt = 0;

struct Aho_Corasick_Automaton{
    int child[maxn][4], fail[maxn], fa[maxn], cnt;
    bool mark[maxn];

    int char2int(char c);
	void calc_fail(); // 见模板
    int count(string s); // 见模板，沿途打标记即可
    void insert(string s){
        int p = 0, len = s.size();
        for(int i=0;i<len;i++){
            int v = char2int(s[i]);
            if(child[p][v] == 0) child[p][v] = cnt++;
            fa[child[p][v]] = p;
            p = child[p][v];
        }
        tail[tcnt++] = p;
    }
}ac;

string exc, buffer;

signed main(){
    int n, m;
    cin >> n >> m >> exc;
    for(int i=0; i<m; i++){
        cin >> buffer;
        slen[i] = buffer.length();
        ac.insert(buffer);
    }
    ac.calc_fail();
    ac.count(exc);
    for(int i=0; i<m; i++){
        int p = tail[i], cnt = 0;
        while(p){
            if(ac.mark[p]) break;
            cnt++;
            p = ac.fa[p];
        }
        cout << slen[i] - cnt << '\n';
    }
}
```






# 参考资料

1.  [强势图解AC自动机](https://www.luogu.com.cn/blog/3383669u/qiang-shi-tu-xie-ac-zi-dong-ji)

