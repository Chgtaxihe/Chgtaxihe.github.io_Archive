---
layout: hidden_page
title: wqs二分学习笔记
---

* auto-gen TOC:
{:toc}




## 算法说明

待补充



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

