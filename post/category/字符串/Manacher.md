---
layout: hidden_page
title: Manacher学习笔记
---

* auto-gen TOC:
{:toc}
# Manacher算法

manacher算法是一个可以在$O(n)$复杂度内求出一个字符串$s$所有**回文子串**的算法。



## 算法步骤

给定一个长度为$n$的字符串$str$，求其所有回文子串



### 预处理

向$str$中插入$n+1$个分隔符（所选的分隔符不能在$str$中出现过），得到串$s$

例如，若$str=abcba$，分隔符为$\#$，则有$s=\#a\#b\#c\#b\#a\#$

这样一来就避免了讨论回文子串的奇偶性



### 计算回文子串

定义数组$d[i]$为串$s$中，以$i$号字符为中心的回文子串的半径。

例如，$s=\#a\#b\#a\#$，则$d=[1,2,1,4,1,2,1]$

显然以$i$为中心的回文子串的长度等于$r[i]-1$

----

在计算$d[0\dots (i-1)]$的过程中，我们维护找到的**最右**（即右边界$r'$最大）回文子串$(l,r)$。

假设$d[0\dots (i-1)]$都已经计算完毕，现在求$r[i]$。

下面分情况讨论

-   若$i>r$，则我们通过朴素算法，一位一位计算

-   否则，有$i\le r$：

    由于串$s_ls_{l+1}\dots s_r$是回文串，令$j=l+(r-i)$，有如下情况
    $$
    \ldots\ \overbrace{ s_l\ \ldots\ \underbrace{ s_{j-d[j]+1}\ \ldots\ s_j\ \ldots\ s_{j+d[j]-1} }_\text{回文子串1}\ \ldots\ \underbrace{ s_{i-d[j]+1}\ \ldots\ s_i\ \ldots\ s_{i+d[j]-1} }_\text{回文子串2}\ \ldots\ s_r }^\text{回文子串}\ \ldots
    $$
    其中回文子串1等于回文子串2

    但由于$i+d[j]-1>r$的位置我们尚未扫描，不知道是否能构成回文子串，因此需要抛弃

    因此有$d[i]=\min(d[l+r-i],r-i+1)$

    接着继续通过朴素算法扫描即可



### 模板(洛谷P3805)

题意：给定字符串$str$，求其最长回文子串的长度

1.47s

```c++
char str[maxn], s[2 * maxn];
int d[2 * maxn];

void solve(){
    cin >> str;
    int len = strlen(str);

    s[0] = '#';
    for(int i=0; i<len; i++){
        s[(i << 1) + 1] = str[i];
        s[(i << 1) + 2] = '#';
    }
    len = (len << 1) + 1;
    s[len] = 0;

    int ans = 0;
    for(int i=1, mid = 0, r = -1; i<len; i++){
        d[i] = (i <= r) ? min(r - i + 1, d[(mid << 1) - i]) : 1;
        while(d[i] <= i && i + d[i] < len && s[i - d[i]] == s[i + d[i]]) d[i]++;
        if(i + d[i] - 1 > r) {
            r = i + d[i] - 1;
            mid = i;
        }
        ans = max(ans, d[i] - 1);
    }
    cout << ans << '\n';

}
```

如果在字符串$s$前再插入一个其他字符（即非分隔符，亦未在$str$中出现过），则可以减少`while`中的条件判断（会快一点点）

1.25s

```c++
void solve(){
    cin >> str;
    int len = strlen(str);

    s[0] = '$', s[1] = '#';
    for(int i=0; i<len; i++){
        s[(i << 1) + 2] = str[i];
        s[(i << 1) + 3] = '#';
    }
    len = (len << 1) + 2;
    s[len] = 0;

    int ans = 0;
    for(int i=1, mid = 0, r = -1; i<len; i++){
        d[i] = (i <= r) ? min(r - i + 1, d[(mid << 1) - i]) : 1;
        while(s[i - d[i]] == s[i + d[i]]) d[i]++;
        if(i + d[i] - 1 > r) {
            r = i + d[i] - 1;
            mid = i;
        }
        ans = max(ans, d[i] - 1);
    }
    cout << ans << '\n';
}
```



# 参考链接

https://oi-wiki.org/string/manacher/

https://www.luogu.com.cn/problem/solution/P3805