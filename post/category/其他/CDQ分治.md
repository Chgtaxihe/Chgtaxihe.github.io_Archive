---
layout: hidden_page
title: CDQ分治学习笔记
---

* auto-gen TOC:
{:toc}




## 算法说明

CDQ分治是一种用来处理多维偏序的好方法，



## 例题 Codeforces 12D

CDQ分治并不比标程慢，就是细节比较多，而且代码量就有点....

由于题目要求是严格小于，需要对CDQ进行一些改造。

1.  对$a$从小到大排序
2.  在进行二分时，由于是严格小于，因而如果要产生贡献，必须有$\forall a_{left},a_{right} \ a_{left} < a_{right}$
3.  在合并的时候，要从后往前遍历，判断左半部分的人是否会suicide，如果会就给他打上标记



为了保证2，我们需要分类讨论一下

1.  如果$a[from]=a[to]$，这一部分不可能产生贡献，因而只需要将其按$b$排序即可
2.  否则，我们要寻找一个分界点$mid$，使得对于$\forall a_i,a_j(from\le i \le mid,mid \lt j \le to), a_i<a_j$，注意细节即可(哭了，细节比想法重要！！)

```c++
#include <bits/stdc++.h>
#define ll long long
#define Android ios::sync_with_stdio(false), cin.tie(NULL)

using namespace std;

const int inf = 0x3f3f3f3f;
const int maxn = 5e5 + 1000;

struct val {
    int a, b, c, idx;
} vals[maxn], tmp[maxn];

bool cmp1(const val & v1, const val & v2){
    if(v1.a == v2.a) {
        if(v1.b == v2.b) return v1.c < v2.c;
        else return v1.b < v2.b;
    }
    return v1.a < v2.a;
}

bool tag[maxn] = {0};
int va[maxn]={0}, _time[maxn]={0};
int dfn = -1, greatest;
vector<int> a, a_pos;

int query(int p) {
    int ret = 0;
    for(int i = p; i > 0; i -= (-i)&i) {
        if(_time[i] != dfn) _time[i] = dfn, va[i] = 0;
        ret += va[i];
    }
    return ret;
}

void add(int p, int delta) {
    for(int i = p; i <= greatest; i += (-i)&i){
        if(_time[i] != dfn) _time[i] = dfn, va[i] = 0;
        va[i] += delta;
    }
}

void cdq(int from, int to, bool contribute) {
    if(from >= to) return;
    int mid = (from + to) >> 1;
    if(!contribute || vals[from].a == vals[to].a){ // 保证左侧一定小于右侧
        contribute = false;
        cdq(from, mid, false), cdq(mid + 1, to, false);
    }else{
        int m1 = lower_bound(a.begin(), a.end(), vals[mid].a + 1) - a.begin();
        if(a_pos[m1]-1 >= to){
            mid = a_pos[m1-1]-1; 
        }else{
            mid = a_pos[m1]-1;
        }
        cdq(from, mid, true), cdq(mid + 1, to, true);
    }

    dfn++;
    int l = mid, r = to, k = to;
    while(l >= from && r > mid) {
        if(vals[r].b > vals[l].b) {
            if(contribute) add(vals[r].c, 1);
            tmp[k--] = vals[r--];
        } else {
            if(contribute) if(query(greatest) - query(vals[l].c) > 0) tag[vals[l].idx] = true;
            tmp[k--] = vals[l--];
        }
    }
    while(l >= from) {
        if(contribute) if(query(greatest) - query(vals[l].c) > 0) tag[vals[l].idx] = true;
        tmp[k--] = vals[l--];
    }
    while(r > mid) tmp[k--] = vals[r--];
    for(int i = from; i <= to; i++) vals[i] = tmp[i];
}

void solve() {
    int n, ans=0;
    cin >> n;
    for(int i = 1; i <= n; i++)  cin >> vals[i].a, vals[i].idx = i;
    for(int i = 1; i <= n; i++)  cin >> vals[i].b;
    // 对c离散化（因为要用树状数组）
    vector<int> unq(n + 1);
    for(int i = 1; i <= n; i++)  {
        cin >> vals[i].c;
        unq[i] = ++vals[i].c; // 树状数组从1开始
    }
    sort(unq.begin(), unq.end());
    unq.resize(unique(unq.begin(), unq.end()) - unq.begin());
    greatest = unq.size() + 3;
    for(int i=1; i<=n; i++) vals[i].c = lower_bound(unq.begin(), unq.end(), vals[i].c) - unq.begin();

    vals[0] = {-1, -1, -1, -1};
    sort(vals + 1, vals + n + 1, cmp1);
    for(int i=1; i<=n; i++){
        if(vals[i].a != vals[i-1].a) {
            a.push_back(vals[i].a);
            a_pos.push_back(i);
        }
    }
    a.push_back(inf);
    a_pos.push_back(n+1);

    cdq(1, n, true);
    for(int i=1; i<=n; i++) if(tag[i]) ans++;
    
    cout << ans << endl;
}

signed main() {
    Android;
    solve();
}
```




