---
layout: hidden_page
title: LCA学习笔记
---

* auto-gen TOC:
{:toc}


# 最近公共祖先

定义：在一棵以$r$为根的树上的两个点$(u,v)$，其最近公共祖先为$u,v$各自到根的路径中，深度最大的公共节点



# 倍增算法（在线）

## 洛谷 P3379

```c++
#include <bits/stdc++.h>
#define Android ios::sync_with_stdio(false), cin.tie(NULL)
using namespace std;

const int maxn = 5e5 + 1000;

const int max_lgn = 20;
int lg[maxn], depth[maxn], up[maxn][max_lgn];
vector<int> G[maxn];
  
void build(int u, int fa, int dep){
    depth[u] = dep;
    for(int i=1; i<max_lgn; i++)
        up[u][i] = up[up[u][i-1]][i-1]; // 倍增
    for(int v:G[u]){
        if(v == fa) continue;
        up[v][0] = u;
        build(v, u, dep + 1);
    }
}

int query(int u, int v){
    if(depth[u] < depth[v]) swap(u, v);

    while(depth[u] > depth[v])
        u = up[u][lg[depth[u] - depth[v]] - 1];
    if(u == v) return u;

    for(int k = lg[depth[u]]; k >= 0; k--){
        if(up[u][k] != up[v][k])
            u = up[u][k], v = up[v][k];
    }
    return up[u][0];
}

void solve(){
    for(int i=1; i<maxn; i++)
        lg[i] = lg[i-1] + (1<<lg[i-1]==i); // log_2(i) + 1

    int n, m, root;
    cin >> n >> m >> root;

    for(int i=1, u, v; i<n; i++){
        cin >> u >> v;
        G[u].push_back(v);
        G[v].push_back(u);
    }

    build(root, 0, 1);

    for(int i=0, u, v; i<m; i++){ // m 个询问
        cin >> u >> v;
        cout << query(u, v) << '\n';
    }
}
  
signed main(){
    Android;
    solve();
}
```





# Tarjan（离线）

[参考资料](https://www.cnblogs.com/JVxie/p/4854719.html)

算法步骤如下：

1.  递归遍历当前节点$u$的所有子节点
2.  检查查询中，与当前节点$u$有关的询问$(u,v)$，若$vis[v]=true$，则$lca(u,v)=getfa(v)$（$getfa(x)$为并查集的函数）
3.  标记当前点，即令$vis[u]=true$，同时，在并查集上将当前节点$u$与其父节点合并

没有太多需要注意的细节



## 洛谷 P3379

内存占用与倍增法相近，耗时比倍增法长($3.30$s)，但胜在代码简单

Ps. 查询也可以使用邻接表储存

```c++
#include <bits/stdc++.h>
#define Android ios::sync_with_stdio(false), cin.tie(NULL)
#define pii pair<int, int>  
using namespace std;

const int maxn = 5e5 + 1000;
int n, m, root;
vector<pii> query[maxn];
vector<int> G[maxn];
int ans[maxn];
int union_set[maxn], vis[maxn];

int get_fa(int x){
    return union_set[x] == x?x:union_set[x] = get_fa(union_set[x]);
}

void tarjan(int u, int fa){
    for(int v:G[u]){
        if(v == fa) continue;
        tarjan(v, u);
        union_set[get_fa(v)] = u;
    }
    for(pii q:query[u]){
        if(!vis[q.second]) continue;
        ans[q.first] = get_fa(q.second);
    }
    vis[u] = true;
}

void solve(){
    cin >> n >> m >> root;

    memset(vis, 0, sizeof vis);
    for(int i=0; i<=n; i++) union_set[i] = i;

    for(int i=1, u, v; i<n; i++){
        cin >> u >> v;
        G[u].push_back(v);
        G[v].push_back(u);
    }

    for(int i=0, u, v; i<m; i++){
        cin >> u >> v;
        query[u].push_back({i, v});
        query[v].push_back({i, u});
    }

    tarjan(root, 0);
    for(int i=0; i<m; i++) cout << ans[i] << '\n';
}

signed main(){
    Android;
    solve();
}
```



