---
layout: hidden_page
title: 2-SAT学习笔记
---

* auto-gen TOC:
{:toc}


# 2-SAT

>   有$n$个布尔$x_1...x_n$，另有$m$个限制条件用以限制$x_i$与$x_j$之间的关系。要求求出一组可行解。

2-SAT就是用来解决以上问题的工具。



## 模板题 洛谷P4782

我们对$x_i$、$\neg x_i$分别建一个点，那么$x_i \lor y_i$就可表示为两条边：$\neg x_i \to y_i$和$\neg y_i \to x_i$

那么我们要怎么表示限制条件$x_i=true$呢？只需让建边$\neg x_i \to x_i$即可

------

得到这么一幅图之后，显然在同一个强连通分量里面的点要么都选，要么都不选

于是我们用`Tarjan`跑一边强连通分量，如果$x_i$与$\neg x_i$在同一个强连通分量，说明无解

------

对于有解的情况，只需输出$x_i$和$\neg x_i$中拓扑序更大的一个即可。

这样能够保证得到解。因为如果存在边$a \to b$，那么一定存在另一条边$\neg b \to \neg a$，因此......（证明略）

（PS.如果用Tarjan"染色"的话，记得得到的颜色是反过来的拓扑序）

AC代码如下：

```c++
#include <bits/stdc++.h>

using namespace std;

const int maxn = 2e6 + 1e3;

int dfn[maxn], low[maxn], steck[maxn], color[maxn]={0};
int color_cnt=0, dfs_n=0, top=0;
stack<int> stk;
vector<int> G[maxn];

void tarjan(int u){
    low[u] = dfn[u] = ++dfs_n;
    stk.push(u);
    for(int v:G[u]){
        if(!dfn[v]) {
            tarjan(v);
            low[u] = min(low[u], low[v]);
        }else if(!color[v]){
            low[u] = min(low[u], low[v]);
        }
    }
    if(low[u] == dfn[u]){
        color_cnt++;
        do{
            u = stk.top(); stk.pop();
            color[u] = color_cnt;
        }while(low[u] != dfn[u]);
    }
}

signed main(){
    ios::sync_with_stdio(false), cin.tie(NULL);
    int n, m, x, a, y, b;
    cin >> n >> m;
    for(int i=0; i<m; i++){
        cin >> x >> a >> y >> b; // x=a or y=b
        G[x + (a^1)*n].push_back(y + b*n); // not x=a then y=b
        G[y + (b^1)*n].push_back(x + a*n); // not y=b then x=a
    }
    for(int i=1; i<=(n<<1); i++) if(!dfn[i]) tarjan(i);
    for(int i=1; i<=n; i++) {
        if(color[i] == color[i+n]){
            cout << "IMPOSSIBLE\n";
            return 0;
        }
    }
    cout << "POSSIBLE\n";
    for(int i=1; i<=n; i++){
        cout << (color[i]>color[i+n]) << " ";
    }
    cout << endl;
}
```





# 参考资料

[2-SAT略解](https://www.luogu.com.cn/blog/user9012/post-2-sat-lve-xie)

[题解 P4782 【【模板】2-SAT 问题】](https://www.luogu.com.cn/blog/user7035/solution-p4782)

