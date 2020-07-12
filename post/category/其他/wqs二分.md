---
layout: hidden_page
title: wqs二分学习笔记
---

* auto-gen TOC:
{:toc}
## 注意事项

要注意的是，要使用wqs二分，则代价函数$cost(x)$（选$x$个/操作$x$次...）必须是一个凸包，即$cost'(x)$单调。（大多数情况下没法严格证明，只能感性猜测或打表）

另外，二分出来的结果不一定正好选择/操作了$k$（题目给定值）次，有几种可能：

1.  二分不对，比如斜率可能为小数，二分时却只考虑了小数
2.  记$g(x)=bias\cdot x+cost(x)$，此时$g'(x)=g'(k)$。不影响，直接按$k$次算即可。

另外，可以将$bias$视作"惩罚"，有助于理解$bias$的作用。



## 例题 洛谷P2619

```c++
/*
    2019-08-21:
         参考:https://www.cnblogs.com/CreeperLKF/p/9045491.htmla
*/
#include <bits/stdc++.h>
#define ll long long
#define Android ios::sync_with_stdio(false), cin.tie(NULL)
using namespace std;

const int maxe = 1e5 + 1000;
const int maxv = 5e4 + 1000;

int bias = 0;
int V, E, need, edge_cnt;
struct edge{
    int u, v, cost, color;
    bool operator <(const edge & e)const{
        // 不能再这里搞事情，应当直接比较
        // 因为当 mid = k -> cnt < need && mid = k+1 -> cnt > need 时，结果是错误的
        // if((color?cost:(cost+bias)) == (e.color?e.cost:(e.cost+bias)))
        //     return color < e.color;
        // return (color?cost:(cost+bias)) < (e.color?e.cost:(e.cost+bias));
        if(cost == e.cost) return color < e.color;
        return cost < e.cost;
    }
}edges[maxe];

struct union_set{
    int u[maxv];

    void clear(int n){for(int i=0; i<=n; i++) u[i] = i;}
    int fa(int nd){return u[nd]==nd?nd:u[nd]=fa(u[nd]);}
    void comb(int a, int b){u[a] = b;}
} uns;

int ans;

int check(int b){
    bias = b;
    for(int i=0;i<E;i++) if(!edges[i].color) edges[i].cost += b;
    sort(edges, edges + E);

    ans = 0;
    uns.clear(V);
    int cnt = 0, disjoint_cnt = V - 1;
    for(int i=0;i<E && disjoint_cnt;i++){
        int a = uns.fa(edges[i].u), b = uns.fa(edges[i].v);
        if(a == b) continue;
        ans += edges[i].cost;
        uns.comb(a, b);
        disjoint_cnt--;
        if(!edges[i].color) cnt++;
    }

    for(int i=0;i<E;i++) if(!edges[i].color) edges[i].cost -= b;
    return cnt;
}

void solve(){
    cin >> V >> E >> need;
    int u, v, cos, col;
    for(int i=0;i<E;i++){
        cin >> u >> v >> cos >> col;
        edges[i] = {u, v, cos, col};
    }

    int l = -120, r = 120, ret = -1;
    while(l <= r){
        int mid = (l + r) / 2; // 相当于斜率
        if(check(mid) >= need){
            ret = ans - need * mid;
            l = mid +1;
        }else{
            r = mid -1;
        }
    }
    cout << ret << endl;
}

signed main(){
    Android;
    solve();
}
```



## New Year and Handle Change (Codeforces 1279F)

一道好题，比赛的时候抄上面的模板过了。赛后仔细思考一下，想明白了几个之前不懂的地方。

$dp$转移很简单，计算小写字母个数时，$dp[i]=min(dp[i-1]+islower(i), dp[i-l]+bias)$。对大写字母同理。



重点在于wqs二分的部分，由于题目的特殊性，wqs二分后，操作数不一定为$k$。

令二分$bias$得到的结果为$ret$，但此时操作次数$cnt[n]$不为$k$（必有$cnt[n]\le k$），下面将简要说明$ans=dp[n]-k*bias$。

记二分得到最终结果为$bias$，对应的操作数$cnt[n]$为$k'$，令$g(k')=bias\cdot k'+op(k')$，其中$op(i)$为操作$i$次时的最优答案（本题中，我们要求的便是$op(k)$）。显然$g(k')=bias\cdot k+op(k)$（否则，二分的最终结果不可能为$k'$）。因此$op(k)=g(k')-bias\cdot k$（而非$g(k')-bias\cdot k'$）。

此处的$g(k')$即为代码中的$dp[n]$

```c++
#include <bits/stdc++.h>
#define ll long long
#define Android ios::sync_with_stdio(false), cin.tie(NULL)
using namespace std;

const int maxn = 1e6 + 1000;

int n, k, l;
char buffer[maxn];
ll dp[maxn], cnt[maxn];

int ck(int p, int pick){
    if(pick == 0) return buffer[p] <= 'Z' && buffer[p] >= 'A';
    return !(buffer[p] <= 'Z' && buffer[p] >= 'A');
}

ll check(ll bias, int pick = 0){
    for(int i=1; i<=n; i++){
        cnt[i] = cnt[i-1];
        dp[i] = dp[i-1] + ck(i, pick);
        if(i < l){
            if(dp[i] > bias){
                dp[i] = bias;
                cnt[i] = 1;
            }
        }else{
            if(dp[i] > dp[i - l] + bias){
                dp[i] = dp[i - l] + bias;
                cnt[i] = cnt[i-l] + 1;
            }
        }
    }
    return cnt[n];
}

void solve(){
    cin >> n >> k >> l;
    cin >> (buffer + 1);
    ll ans = n;

    for(int pic=0; pic<2; pic++){
        ll l = 0, r = n + 10, mid, ret = r;
        while(l <= r){
            mid = (l + r) >> 1;
            if(check(mid, pic) <= k){
                ret = mid;
                r = mid - 1;
            }else{
                l = mid + 1;
            }
        }
        check(ret, pic);
        ans = min(ans, dp[n] - k * ret);
    }
    cout << ans << '\n';
}

signed main(){
    Android;
    solve();
}
```

