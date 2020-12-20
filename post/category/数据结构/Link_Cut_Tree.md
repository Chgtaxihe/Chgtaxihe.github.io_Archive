---
layout: hidden_page
title: Link Cut Tree学习笔记
---

* auto-gen TOC:
{:toc}


# Link/Cut Tree(动态树)

[Wiki](https://en.wikipedia.org/wiki/Link/cut_tree)定义

>   A **link/cut tree** is a data structure for representing a forest, a set of rooted trees, and offers the following operations:
>
>   -   Add a tree consisting of a single node to the forest.
>   -   Given a node in one of the trees, disconnect it (and its subtree) from the tree of which it is part.
>   -   Attach a node to another node as its child.
>   -   Given a node, find the root of the tree to which it belongs. By doing this operation on two distinct nodes, one can check whether they belong to the same tree.

可以看成是高级版的并查集(Union find set)



## 辅助树

由Splay树构成，每棵辅助树维护的是一棵树，一些辅助树构成的森林，即LCT

有以下性质

1.  原树中的每个节点与辅助树中Splay节点一一对应

2.  每个Splay维护的是在原树中深度**严格递增**的路径，**中序遍历**Splay得到的每个点深度严格递增（Splay树性质）

3.  边分为**实边**和**虚边**，实边包含在Splay中，虚边则由一棵Splay指向**另一棵**Splay上的某一节点（指向该Splay中**深度最小**的节点的父节点）

    在这里，设子节点为$x$，其父节点为$y$，则定有$fa[x]=y$，若有$ch[y][0/1]=x$则该边为实边，否则为虚边

**为了解题，splay有时还会维护一下size属性**



## 变量定义

```
// fa[x]: 该splay节点的父节点, ch[x][0/1]: splay树中x的左/右子节点
```



## splay(x)

作用：将x旋转到其splay树的根

### 辅助函数 is_root(x)

作用：splay的辅助函数，判断x是否为splay的根

```c++
#define isroot(x) (ch[fa[x]][0] != x && ch[fa[x]][1] != x)
```

若父节点的左/右子节点均不是自己，那么就是根啦

### 辅助函数 chk(x)

```c++
#define chk(x) (ch[fa[x]][1] == x) /* 是否为父节点的右子节点 */
```

### 辅助函数rotate(x)

作用：splay树中标准的旋转函数

```c++
void rotate(int x){
    int y = fa[x], z = fa[y], k = chk(x), v = ch[x][!k];
    if(!isroot(y)) ch[z][chk(y)] = x;
    ch[x][!k] = y, ch[y][k] = v;
    if(v) fa[v] = y;
    fa[y] = x, fa[x] = z;
    pushup(y);
    pushup(x);
}
```

### 辅助函数 update(x)

作用：从根节点一路pushdown到当前节点

也可以用手工栈代替递归栈

```c++
void update(int x){ // 从splay根节点一路pushdown
	if(!isroot(x)) update(fa[x]);
    pushdown(x);
}
```

### 辅助函数pushdown/pushup

```c++
void pushup(int x){xor_sum[x] = w[x] ^ xor_sum[ch[x][0]] ^ xor_sum[ch[x][1]];}
void pushdown(int x){ // 注意这里pushdown的写法
    // 由于flip会打上标记同时翻转，因此pushdown时就不必翻转了
    if(r[x] == 0) return;
    r[x] = 0;
    if(ch[x][0]) flip(ch[x][0]);
    if(ch[x][1]) flip(ch[x][1]);
}
```



### splay函数：

```c++
void splay(int x){ // 将x旋转到其所在splay树的根部
    update(x); // 也可以用手工栈代替
    while(!isroot(x)){ // splay双旋
        int y = fa[x];
        if(!isroot(y)) rotate(chk(x)==chk(y)?y:x);
        rotate(x);
    }
}
```



## access(x)

作用：删除x到根路径上所有连向其他点的重链，重新拉一条x到根（原树的根）的重链（实链）。

注：在新拉出来的链中，原树中深度最大的点为x

```c++
// fa[x]: 该splay节点的父节点, ch[x][0/1]: splay树中x的左/右子节点
void access(int x){
    for(int y=0; x; y = x, x = fa[x]){
        splay(x); // 将该节点旋到其所在的splay树的根节点
        ch[x][1] = y; // 实链更新
        pushup(x); // 子节点变了，更新信息
    }
}
```



## make_root(x)

作用：将x到（原树）根节点路径上的点全部翻转（即路径上的节点深度翻转，x成为深度最小的点）

副作用：x成为splay的根

```c++
void flip(int x){ // splay的翻转操作
    swap(ch[x][0], ch[x][1]);
    r[x] ^= 1; // 翻转标记(不打标记会破坏深度关系)
}

void makeroot(int x){
    access(x); // 先将根节点与x接到同一颗splay树中
    splay(x); // 旋到splay的根节点，此时定有ch[x][1] == 0
    flip(x); // 翻转
}
```



## split(x, y)

作用：将x到y的路径合并到同一颗splay树中

副作用：x成为原树的根节点，y成为splay的根节点

```c++
void split(int x, int y){
    makeroot(x); // 原树换根
    access(y); // x与y并到一棵splay中
    splay(y); // 将y旋到splay树根节点
}
```



## find_root(x)

作用：寻找x在原树中的树根（可用于判断两节点间是否连通）

副作用：原树的根成为splay的根

```c++
int findroot(int x){
    access(x); // 先将根节点与x接到同一颗splay树中
    splay(x); // 旋到splay的根节点
    while(ch[x][0]) pushdown(x), x = ch[x][0]; // 不断向左走，下放信息
    // 下放信息似乎是不必要的，因为splay(x)的时候已经进行了update(x)
    splay(x); // 保证复杂度???
    return x; // 由辅助树的性质可知，中序遍历的第一个节点即为根节点
}
```



## link(x, y)

作用：将x与y在原图（森林）中连接起来

副作用：x成为原树的根

```c++
bool link(int x, int y){
    makeroot(x); // x成为其所在树的树根, 此时fa[x] == 0
    // 若y与x在原图中是联通的（在同一颗树上），建边不合法
    if(findroot(y) == x) return false; 
    return fa[x] = y, true; // 建立一条虚边
}
```



## cut(x, y)

作用：将x到y的边断开。

副作用：x成为原树及splay树的根

```c++
bool cut(int x, int y){
    makeroot(x);
    // 若存在边(x,y)，则: (x,y)联通，且(x,y)路径上没有其他链，且y没有左儿子
    // 注意side_effects: 在findroot(y)后，x成为splay的根
    if(findroot(y) != x || fa[y] != x || ch[y][0] != 0) return false;
    fa[y] = ch[x][1] = 0; // 断开边
    pushup(x); // 更新信息
    return true;
}
```



# 例题引入 洛谷P3690



给定 $n$ 个点以及每个点的权值，要你处理接下来的 $m$ 个操作。 操作有四种，操作从 0 到 3 编号。点从 1 到 $n$ 编号。

- `0 x y` 代表询问从 $x$ 到 $y$ 的路径上的点的权值的 xor 和。保证 $x$ 到 $y$ 是联通的。
- `1 x y` 代表连接 $x$ 到 $y, \quad$ 若 $x$ 到 $y$ 已经联通则无需连接。
- `2 x y` 代表删除边 $(x, y),$ 不保证边 $(x, y)$ 存在。
- `3 x y` 代表将点 $x$ 上的权值变成 $y$。



AC代码(0.983 s)

```c++
#include <bits/stdc++.h>
#define ll long long
#define Android ios::sync_with_stdio(false), cin.tie(NULL)
using namespace std;

const int maxn = 3e5 + 1000;

ll w[maxn], n, m;

struct link_cut_tree{
    int ch[maxn][2], fa[maxn], r[maxn];
    ll xor_sum[maxn];

    int _stack[maxn]; // 手工栈

    #define isroot(x) (ch[fa[x]][0] != x && ch[fa[x]][1] != x)
    #define chk(x) (ch[fa[x]][1] == x) /* 是否为父节点的右子节点 */

    // splay函数
    void pushup(int x){xor_sum[x] = w[x] ^ xor_sum[ch[x][0]] ^ xor_sum[ch[x][1]];}
    void pushdown(int x){ // 注意这里pushdown的写法
        if(r[x] == 0) return;
        r[x] = 0;
        if(ch[x][0]) flip(ch[x][0]);
        if(ch[x][1]) flip(ch[x][1]);
    }
    void flip(int x){ // splay的翻转操作
        swap(ch[x][0], ch[x][1]);
        r[x] ^= 1; // 翻转标记(不是很懂，不打标记也不会破坏原树的连接关系呀)
    }

    void rotate(int x){
        int y = fa[x], z = fa[y], k = chk(x), v = ch[x][!k];
        if(!isroot(y)) ch[z][chk(y)] = x;
        ch[x][!k] = y, ch[y][k] = v;
        if(v) fa[v] = y;
        fa[y] = x, fa[x] = z;
        pushup(y);
        pushup(x);
    }

    void update(int x){ // 从splay根节点一路pushdown
        if(!isroot(x)) update(fa[x]);
        pushdown(x);
    }

    void splay(int x){
        // update(x); 
        // 手工栈代替update函数
        int top = 0, f = x; _stack[top++] = x;
        while(!isroot(f)) _stack[top++] = f = fa[f];
        while(top) pushdown(_stack[--top]);

        while(!isroot(x)){ // splay双旋
            int y = fa[x];
            if(!isroot(y)) rotate(chk(x)==chk(y)?y:x);
            rotate(x);
        }
    }

    #undef isroot
    #undef chk

    // lct函数

    void access(int x){
        // fa[x]: 该splay节点的父节点, ch[x][0/1]: splay树中x的左/右子节点
        for(int y=0; x; y = x, x = fa[x]){
            splay(x); // 将该节点旋到其所在的splay树的根节点
            ch[x][1] = y; // 实链更新
            pushup(x); // 子节点变了，更新信息
        }
    }

    void makeroot(int x){
        access(x); // 先将根节点与x接到同一颗splay树中
        splay(x); // 旋到splay的根节点，此时定有ch[x][1] == 0
        flip(x); // 翻转
    }

    void split(int x, int y){
        makeroot(x); // 原树换根
        access(y); // x与y并到一棵splay中
        splay(y); // 将y旋到splay树根节点
    }

    int findroot(int x){
        access(x); // 先将根节点与x接到同一颗splay树中
        splay(x); // 旋到splay的根节点
        while(ch[x][0]) pushdown(x), x = ch[x][0]; // 不断向左走，下放信息
        splay(x); // 保证复杂度???
        return x; // 由辅助树的性质可知，中序遍历的第一个节点即为根节点
    }

    bool link(int x, int y){
        makeroot(x); // x成为其所在树的树根, 此时fa[x] == 0
        // 若y与x在原图中是联通的（在同一颗树上），建边不合法
        if(findroot(y) == x) return false; 
        return fa[x] = y, true; // 建立一条虚边
    }

    bool cut(int x, int y){
        makeroot(x);
        // 若存在边(x,y)，则: (x,y)联通，且(x,y)路径上没有其他链，且y没有左儿子
        // 注意side_effects: 在findroot(y)后，x成为splay的根
        if(findroot(y) != x || fa[y] != x || ch[y][0] != 0) return false;
        fa[y] = ch[x][1] = 0; // 断开边
        pushup(x); // 更新信息
        return true;
    }

}lct;

void solve(){
    cin >> n >> m;
    for(int i=1; i<=n; i++) {
        cin >> w[i];
        lct.xor_sum[i] = w[i];
    };
    for(int i=0, op, x, y; i<m; i++){
        cin >> op >> x >> y;
        if(op == 0){
            lct.split(x, y);
            cout << lct.xor_sum[y] << '\n';
        }
        if(op == 1) lct.link(x, y);
        if(op == 2) lct.cut(x, y);
        if(op == 3){
            lct.splay(x);
            w[x] = y;
            lct.pushup(x);
        }
    }
}

signed main(){
    redirect_input;
    Android;
    solve();
}
```



# 其他技巧

## 求LCA

稍微修改一下`access(x)`函数

```c++
int access(int x){
    int y = 0; // 其实就改了这里
    for(; x; y = x, x = fa[x]){
        splay(x);
        ch[x][1] = y;
        pushup(x);
    }
    return y; // 返回最后一个访问到的
}
```



求$(u,v)$的lca前先`makeroot`确定树根，再`access(x)`，那么`lca=access(y)`

解析：

记$access(x)$后，根节点$root$所在的splay树为$t_1$，$access(y)$后根节点所在的splay树为$t_2$，则$t_1$与$t_2$共有的点即为$x\to root,y\to root$路径上的公共节点，$access(y)$过程中访问到的第一个公共点（该点同时为深度最大的公共节点）即为$lca(x,y)$



洛谷P3379 AC代码（截取）

比树剖省空间（23MB/8MB），但是很慢（1.27s/2.79s）

```c++
void solve(){
    int n, m, s;
    cin >> n >> m >> s;
    for(int i=1, u, v; i<n; i++){
        cin >> u >> v;
        lct.link(u, v);
    }
    lct.makeroot(s);
    for(int i=0, u, v; i<m; i++){
        cin >> u >> v;
        lct.access(u);
        cout << lct.access(v) << '\n';
    }
}
```



# 非旋treap维护LCT

等我先学会treap



# 练习题

| **题目**                                                     | **完成情况** | **备注**                                                     |
| ------------------------------------------------------------ | ------------ | ------------------------------------------------------------ |
| **LCT上平衡树操作**                                          |              |                                                              |
| [[HNOI2010]弹飞绵羊](https://www.luogu.com.cn/problem/P3203) | AC           | 这题我做过，当时是用分块AC的。LCT的话，Splay上维护一下size即可 |
| [[国家集训队]Tree II](https://www.luogu.com.cn/problem/P1501) | AC           | 正确维护splay即可（为什么我的代码就是又臭又长呢）            |
|                                                              |              |                                                              |
| **维护连通性**                                               |              |                                                              |
| [部落冲突](https://www.luogu.com.cn/problem/P3950)           | AC           | 不用在splay上维护额外信息，爽！                              |
| [[AHOI2005] 航线规划](https://www.luogu.com.cn/problem/P2542) |              | 据说LCT维护双联通只支持加边？（那用树剖不就得了...）         |



# 参考

https://www.cnblogs.com/flashhu/p/8324551.html

https://oi-wiki.org/ds/lct

https://www.luogu.com.cn/blog/Qiu/qian-tan-link-cut-treeQ