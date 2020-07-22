---
layout: hidden_page
title: Lyndon分解学习笔记
---

* auto-gen TOC:
{:toc}
# Lyndon 串 (Lyndon word)

一个串是 Lyndon 串，当且仅当这个串的最小后缀就是这个串本身。

在 Wiki 上还有另外一个等价的定义：串$S$是其所有循坏位移中最小的一个。（见[Wiki](https://en.wikipedia.org/wiki/Lyndon_word)）



# Lyndon 分解

将字符串$S$分解成$S=s_1s_2\cdots s_m$，使得所有$s_i$都为 `Lyndon word`，且$\forall 1\le i\le m,s_i\ge s_{i+1}$。



注意：在本文中，所有对字符串进行的`+`操作均代表连接两个字符串



## 引理1. 若$u,v$都是Lyndon串且$u<v$，则$uv$也是Lyndon串

1.  若$\mid u\mid \ge \mid v\mid$

    ​	显然$u[:\mid v\mid]<v$，因此$uv<v$。

2.  若$\mid u\mid <\mid v\mid$

    1.  $u$为$v$的前缀时，若$v<uv$，则有$v[\mid u\mid + 1:]<v$，矛盾
    2.  $u$不为$v$的前缀时，显然

易得$u[i:] + v > u + v\ (i>0)$。

由于$v>uv$，且$v$为Lyndon串，因此$v$的所有后缀都大于$uv$。



## 引理2. Lyndon分解存在且唯一

初始令 $m=|S|$ 并且 $A_{i}=S[i],$ 然后每次不断找到 $A_{i}<A_{i+1}$ 并且合并为一个串（由**引理1**可知，合并后的串为仍为Lyndon串）。最后一定能使得所有的 $A_{i} \geq A_{i+1}$ 。

存在性得证。

------

假设存在两个Lyndon分解，分别为

$$
\begin{align}
S_n &= s_1 s_2 \cdots s_i s_{i+1} \cdots s_{m_1} \tag{1}\\
S_n &= s_1 s_2 \cdots s'_i s'_{i+1} \cdots s'_{m_2} \tag{2}
\end{align}
$$

不妨令$\mid s_i\mid>\mid s'_i\mid$，则$s_i=s'_i s'_{i+1}\cdots s'_{j-1} + s'_{j}[:l]\ (l\le\mid s'_j\mid)$，且$s'_i<s_i$

由Lyndon性质可知：$s_i<s'_j[:l]$

又因为$s'_j[:l]$为$s'_j$的前缀，因此$s'_j[:l]\le s'_j$

根据划分$(2)$，可知$s'_j\le s'_i$

最终得到“不等式”：$s'_i<s_i< s'_j[:l]\le s'_j\le s'_i$，“不等式”矛盾。

唯一性得证。



## 引理3. 若串$v$与字符$c$满足$vc$是某个Lyndon串的前缀，则对于字符$d>c$，$vd$是Lyndon串

设该Lyndon串为$v+c+t$，则$v[i:]+c+t>v+c+t\ (i>0)$，因此$v[i:]+d>v+d>v+c+t$。

又因为$c>v[0]$，因此$d>v+d$。

故$v+d$为Lyndon串。



## Duval 算法

维护3个指针$i,j,k$。

-   $S[:i-1]=s_1s_2\cdots s_g$为已经固定的（处理好了的）分解。
-   $S[i,k-1]=t^h + v$为尚未固定的分解，满足串$t$是Lyndon串，$v$为$t$的可为空的前缀且$v\ne t$。

![](https://blog.chgtaxihe.top/resource/img/post/Lyndon分解_1.png)



当前读入$S[k]$，令$j=k-\mid t \mid$

-   若$S[k]>S[j]$，由于$v$为$t$的前缀，根据**引理3**可知，$v+S[k]$为Lyndon串。

    但此时若单独划分出$v+S[k]$，并不能满足$s_i\ge s_{i+1}$的划分要求，因此要与前面所有$t$合并。

    最终得到**新的Lyndon串**$t' =t^h+v+S[k]$ 。但此时**不能确定**该串是否为一个独立的划分。

-   若$S[k]=S[j]$，可知周期继续，令$k=k+1,j=j+1$即可。

-   若$S[k]<S[j]$，显然$t^h+v+S[k]$不是Lyndon串，此时前面$t$的分解固定了，算法从$v$的开头继续。



时间复杂度$O(n)$



### 例题: 洛谷 P6114

给定一个串$S$，求其Lyndon划分，并输出一个整数，代表所有右端点(1-indexed)的异或和。

AC代码

```c++
#include <bits/stdc++.h>
using namespace std;

const int maxn = 5e6 + 1000;

char s[maxn];
int len, ans = 0;

signed main(){
    cin >> (s + 1);
    len = strlen(s + 1);

    int i = 1, j, k;
    while(i <= len){
        j = i, k = i + 1;
        while(k <= len && s[k] >= s[j]){
            j = (s[k]==s[j])?j+1:i;
            k++;
        }
        while(i <= j){ // j < 串v开头的位置
            ans ^= i + (k - j) - 1;
            i += k - j; // k - j: 循环节长度
        }
    }
    cout << ans << '\n';
}
```



# 参考

-   [题解 P6127](https://www.luogu.com.cn/blog/wucstdio/solution-p6127)
-   [题解 P6114](https://www.luogu.com.cn/blog/blog10086001/ssssolution-p6114)
-   [Wiki](https://en.wikipedia.org/wiki/Lyndon_word)


