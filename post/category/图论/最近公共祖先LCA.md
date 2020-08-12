---
layout: hidden_page
title: LCA学习笔记
---

* auto-gen TOC:
{:toc}


# 最近公共祖先

定义：在一棵以$r$为根的树上的两个点$(u,v)$，其最近公共祖先为$u,v$各自到根的路径中，深度最大的公共节点



# 倍增算法（在线）

## 洛谷 P3379 (2.13s, 69.81MB)

用邻接表存图会快很多！

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



## 洛谷 P3379 (1.89s, 41.66MB)

不能在线处理，但胜在代码简单

Ps. 查询也可以使用邻接表储存

```c++
#include <bits/stdc++.h>
#define Android ios::sync_with_stdio(false), cin.tie(NULL)
#define pii pair<int, int>  
using namespace std;

const int maxn = 5e5 + 1000;
int n, m, root;
vector<pii> query[maxn];
int head[maxn], nxt[2 * maxn], dest[2 * maxn], edge_cnt = 0;
int ans[maxn];
int union_set[maxn], vis[maxn];

int get_fa(int x){
    return union_set[x] == x?x:union_set[x] = get_fa(union_set[x]);
}

void add_edge(int u, int v){
    nxt[++edge_cnt] = head[u];
    dest[edge_cnt] = v;
    head[u] = edge_cnt;
}

void tarjan(int u, int fa){
    for(int x=head[u]; x; x=nxt[x]){
        if(dest[x] == fa) continue;
        tarjan(dest[x], u);
        union_set[get_fa(dest[x])] = u;
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
        add_edge(u, v);
        add_edge(v, u);
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



# 树链剖分(在线)

没想到树剖居然这么快！

但能不剖就不剖

## 洛谷 P3379 (1.27s, 23.75MB)

```c++
#include <bits/stdc++.h>
#define Android ios::sync_with_stdio(false), cin.tie(NULL)
using namespace std;

struct heavy_light_seg{
    static const int max_node = 5e5 + 100;
    // 储存原图
    int head[max_node], nxt[max_node * 2], dest[max_node * 2];
    int n, edge_cnt, root;
    // 原图信息
    int size[max_node], fa[max_node], heavy_son[max_node], depth[max_node];
    // 重链剖分
    int dfn;
    int top[max_node], id_node[max_node], node_id[max_node];

    void init(int node_cnt){
        n = node_cnt;
        edge_cnt = dfn = 0;
        for(int i=0; i<=n; i++) head[i] = 0, heavy_son[i] = -1;
    }

    inline void add_edge(int u, int v){ // 原图的边
        dest[++edge_cnt] = v;
        nxt[edge_cnt] = head[u];
        head[u] = edge_cnt;
    }

    void _dfs1(int u, int parent, int dep){
        size[u] = 1;
        fa[u] = parent;
        depth[u] = dep;
        int & hs = heavy_son[u];
        for(int x=head[u]; x; x=nxt[x]){
            if(dest[x] == parent) continue;
            _dfs1(dest[x], u, dep + 1);
            size[u] += size[dest[x]];
            if(hs == -1 || size[hs] < size[dest[x]]) hs = dest[x];
        }
    }

    void _dfs2(int u, int t){ // 按dfs序编号
        top[u] = t;
        node_id[u] = ++dfn;
        id_node[dfn] = u;

        if(heavy_son[u] == -1) return; // 叶子节点
        _dfs2(heavy_son[u], t); // 先遍历重子节点,使dfs序连续
        for(int x=head[u]; x; x=nxt[x]){
            if(dest[x] == fa[u] || dest[x] == heavy_son[u]) continue;
            _dfs2(dest[x], dest[x]);
        }
    }

    void build(int rt){
        root = rt;
        _dfs1(root, -1, 1);
        _dfs2(root, root);
    }

    int lca(int u, int v){
        while(top[u] != top[v]){ // 不在同一条链上
            if(depth[top[u]] > depth[top[v]]) swap(u, v);
            v = fa[top[v]];
        }
        return depth[u] < depth[v]?u:v;
    }
}hls;

void solve(){
    int n, m, s;
    cin >> n >> m >> s;
    hls.init(n);
    for(int i=1, u, v; i<n; i++){
        cin >> u >> v;
        hls.add_edge(u, v);
        hls.add_edge(v, u);
    }
    hls.build(s);
    for(int i=0, u, v; i<m; i++){
        cin >> u >> v;
        cout << hls.lca(u, v) << '\n';
    }
}

signed main(){
    Android;
    solve();
}
```

