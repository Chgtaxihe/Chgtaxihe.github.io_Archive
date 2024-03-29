---
layout: hidden_page
title: Splay学习笔记
tags: algorithm data_structure splay
---

* auto-gen TOC:
{:toc}

# Splay树学习笔记1 区间翻转

### 前言
很早之前就想学Splay，但是一看到树上旋转就头晕 ╮(╯﹏╰）╭

直到做数据结构课设（AVL树）那天我才感受到什么才是真正的恐怖~ wsl

### Splay简介
Splay树是一种二叉搜索树，操作均摊复杂度为 O(log n) (不会证)，同时由于Splay操作的存在，Splay树做区间翻转也是很好用的~

注意，本文只会涉及到区间翻转，至于其他的应用，大概会放到下一篇笔记里吧。。

### 前置知识
AVL树（吧？）、线段树

### 旋转操作
大家在数据结构应该都学过，二叉搜索树的形状与插入数据的顺序有关，即二叉搜索树在某些情况下会退化成一条链，这个时候我们可以通过旋转进行优化。Splay树的旋转也相似。

下面直接贴代码：

```c++
inline void push_up(int rt){
    size[rt] = size[child[rt][0]] + size[child[rt][1]] + 1;
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
    push_up(p), push_up(rt); // 不知道为什么先pushup(rt)再pushup(p)也能AC
}
```

`par[x]`指的是`x`节点的父节点,`child[x][0/1]`是`x`节点的左/右子节点

其中`chk(int rt)`是辅助函数，用于判断节点rt是父节点的左子节点还是右子节点。 
相信学过AVL树的同学应该都能看懂，详细的解析以后补上（先挖个坑）

### Splay操作
Splay操作并不复杂，他的作用是将节点rt一直向根节点方向旋转，直到其成为`goal`的子节点

代码如下:

```c++
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
```
当rt、父节点、父节点的父节点(下面简称"爷节点")连成一条直线时，先旋转父节点，再旋转子节点有利于降低深度(挖坑)。
这里要注意的是，当`rt`的爷节点是`goal`时，我们应当直接旋转`rt`两次。

另外，可以证明的是，splay操作不会影响树的中序遍历结果。

那么问题来了，如果goal的深度大于rt，会发生什么呢？(wa_keng)

**UPD:** 双旋操作在树的层数（高度）小于5时似乎是没有意义的。



### 区间翻转

先上一道例题 [洛谷P3391]("https://www.luogu.org/problem/P3391")

容易想到，对一个区间进行翻转，只需要递归交换节点`rt`的左右子树即可(想象一下，我就不画图了 ヽ(￣▽￣)ﾉ )，那么，只要我们找到一颗只含有 [l, r] 区间内节点的子树，我们就可以轻易解决问题！

如何构建这样子的子树呢？我们只要找到 l的前驱， r的后继，那么在这两者之间的点便都是区间 [l, r] 内的点。结合splay操作，可以得到以下代码

```c++
//寻找第pos个数字
int find(int pos){
    int cur = root;
    while(cur){
        if(size[child[cur][0]] >= pos){
            cur = child[cur][0];
        }else if(size[child[cur][0]] + 1 >= pos){
            return cur;
        }else{
            pos -= size[child[cur][0]] + 1;
            cur = child[cur][1];
        }
    }
    //没找到节点，说明输入的pos有误
    assert(false);
    return -1;
}

void reverse(int l, int r){
    r += 2;//+2 是因题目需要，建树时额外插入了一个点
    l = find(l), r = find(r);
    splay(l, 0), splay(r, l);
    递归旋转(child[r][0]);
}
```

将`l`的前驱作为根节点，将`r`的后继接在根节点的右方，那么`r`的左子树便是我们想要得到的。

等等，要是每次`reverse`都得遍历一遍`child[r][0]`的子节点，那复杂度不得爆炸？

像这样

![超时](https://blog.chgtaxihe.top/resource/img/post/al_ds_splay1_2019-07-25_01.PNG)

于是改进代码

```cpp
inline void push_down(int rt){
    if(!tag[rt]) return;
    tag[child[rt][0]] ^= 1;
    tag[child[rt][1]] ^= 1;
    swap(child[rt][0], child[rt][1]);
    tag[rt] = 0;    
}

int find(int pos){
    int cur = root;
    while(cur){
        //对每个splay路径上的点做一次pushdown
        push_down(cur);
        if(size[child[cur][0]] >= pos){
            cur = child[cur][0];
        }else if(size[child[cur][0]] + 1 >= pos){
            return cur;
        }else{
            pos -= size[child[cur][0]] + 1;
            cur = child[cur][1];
        }
    }
    assert(false);
    return -1;
}

void reverse(int l, int r){
    r += 2;
    l = find(l), r = find(r);
    splay(l, 0), splay(r, l);
    tag[child[r][0]] ^= 1;
}

```

我们给每个点打上标记，类似于线段树的lazy标记(别忘了`push_down`)。

### P3391 完整代码

```c++
#include <bits/stdc++.h>
#define Android ios::sync_with_stdio(false), cin.tie(NULL)
#define ll long long

using namespace std;

const int maxn=1e5+500;

int child[maxn][2], val[maxn], par[maxn], tag[maxn]={0}, size[maxn]={0};
int root, nrof_node = 0;

inline void push_up(int rt){
    size[rt] = size[child[rt][0]] + size[child[rt][1]] + 1;
}

inline void push_down(int rt){
    if(!tag[rt]) return;
    tag[child[rt][0]] ^= 1;
    tag[child[rt][1]] ^= 1;
    swap(child[rt][0], child[rt][1]);
    tag[rt] = 0;    
}

int build_tree(int l, int r, int p){
    if(l > r) return 0;
    int idx = ++nrof_node;
    int mid = (l + r)>>1;
    val[idx] = mid, par[idx] = p;
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
    push_up(p), push_up(rt); // 不知道为什么先pushup(rt)再pushup(p)也能AC
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
        //对每个splay路径上的点做一次pushdown
        push_down(cur);
        if(size[child[cur][0]] >= pos){
            cur = child[cur][0];
        }else if(size[child[cur][0]] + 1 >= pos){
            return cur;
        }else{
            pos -= size[child[cur][0]] + 1;
            cur = child[cur][1];
        }
    }
    assert(false);
    return -1;
}

void reverse(int l, int r){
    r += 2;
    l = find(l), r = find(r);
    splay(l, 0), splay(r, l);
    tag[child[r][0]] ^= 1;
}

int n;
//中序遍历，别忘了push_down
void dfs(int rt){
    push_down(rt);
    if(child[rt][0]) dfs(child[rt][0]);
    if(val[rt] != 0 && val[rt] != n+1) cout << val[rt] << ' ';
    if(child[rt][1]) dfs(child[rt][1]);
}

void solve(){
    int m, a, b;
    cin >> n >> m;
    //额外插入了两个点(0 和 n+1)
    root = build_tree(0, n+1, 0);

    for(int i=0;i<m;i++){
        cin >> a >> b;
        reverse(a, b);
    }

    dfs(root);
    cout << endl;
}

int main(){
    Android;
    solve();
}

```



# Splay学习笔记2 应用篇A

## 前言

昨天学了Splay树的一些基本操作，今天就来实际运用一下（当然不能是那种正经的应用啦～）

## Splay模拟线段树

原题链接 [洛谷P3372](https://www.luogu.org/problem/P3372)

这是一道线段树的模板题

还是继续用Splay的模板，不过这次我们的标记改成了`Lazy`，用来保存区间变化值，同时用`sum[x]`来保存以`x`为根的子树的和。于是当我们想要求区间和的时候，只需要像`reverse`一样，把区间左端点的前驱、区间右端点的后继给Splay一下，那么答案就是`sum[ child[ child[current_root][1] ][0] ]`(语言乏力，凑合着看吧)

## 耗时

使用正经线段树的耗时

![使用正经线段树的耗时](https://blog.chgtaxihe.top/resource/img/post/al_ds_splay2_01.png)

使用Splay的耗时

![使用Splay的耗时](https://blog.chgtaxihe.top/resource/img/post/al_ds_splay2_02.png)

## AC代码

```c++
/*
    2019-07-30:
        正经线段树耗时:531ms
        Splay耗时:1.13s
*/

#include <bits/stdc++.h>
#define Android ios::sync_with_stdio(false), cin.tie(NULL)
#define ll long long

using namespace std;
//并不需要四倍空间 QAQ
const int maxn=1e5+500;

int child[maxn][2], val[maxn], par[maxn], size[maxn]={0};
ll lazy[maxn]={0}, sum[maxn]={0}, v[maxn];
int root, nrof_node = 0;

inline void push_up(int rt){
    size[rt] = size[child[rt][0]] + size[child[rt][1]] + 1;
    sum[rt] = val[rt] + sum[child[rt][0]] + sum[child[rt][1]];
}

inline void add(int rt, ll delta){
	if(!rt) return;
	lazy[rt] += delta;
	val[rt] += delta;
	sum[rt] += delta * size[rt];
}

inline void push_down(int rt){
    if(!lazy[rt]) return;
    add(child[rt][0], lazy[rt]);
    add(child[rt][1], lazy[rt]);
    lazy[rt] = 0;
}

int build_tree(int l, int r, int p){
    if(l > r) return 0;
    int idx = ++nrof_node;
    int mid = (l + r)>>1;
    val[idx] = v[mid], par[idx] = p;
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
    push_up(p), push_up(rt); // 不知道为什么先pushup(rt)再pushup(p)也能AC
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
        //对每个splay路径上的点做一次pushdown
        push_down(cur);
        if(size[child[cur][0]] >= pos){
            cur = child[cur][0];
        }else if(size[child[cur][0]] + 1 >= pos){
            return cur;
        }else{
            pos -= size[child[cur][0]] + 1;
            cur = child[cur][1];
        }
    }
    //没找到节点，说明输入的pos有误
    assert(false);
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
    return sum[child[r][0]];
}


void solve(){
    int n, m;
    cin >> n >> m;
    for(int i=1;i<=n;i++) cin >> v[i];

    //额外插入两个点
    root = build_tree(0, n+1, 0);
	int op, x, y, k;
    for(int i=0;i<m;i++){
        cin >> op;
        if(op == 1){
        	cin >> x >> y >> k;
        	interval_add(x, y, k);
        }else{
        	cin >> x >> y;
        	cout << interval_query(x, y) << '\n';
        }
    }

}

int main(){
    //redirect_input();
    Android;
    solve();
}

```



# 习题

### [POJ3468](https://blog.chgtaxihe.top/post/Splay/POJ3468.html)