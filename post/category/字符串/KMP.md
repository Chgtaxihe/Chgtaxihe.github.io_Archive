---
layout: hidden_page
title: KMP/扩展KMP学习笔记
---

* auto-gen TOC:
{:toc}
# 前言

突然发现自己kmp算法掌握得不是很到位。写一篇笔记就当复习好了。



# KMP

$fail[i]$指向的是**当前位失配时，与模式串前缀相同的最长后缀**，也是下一次配对的位置

举个例子，当计算$fail$指针时，假设模式串$pat$为"ababc"

则$fail[]=\{0, 0, 1, 2, 0\}$



一个容易理解的算法，并不需要太多解析。

## 模板

```c++
#include <bits/stdc++.h>
using namespace std;

char ori[1000050], pattern[1000050];
int f[1000050], l1, l2;
void calc(){
    int k=0;
    f[0]=f[1]=0;
    for(int i=1; i<l2; i++) {
        while(k && pattern[i]!=pattern[k]) k=f[k];
        //无下面这一行代码则应称为MP算法
        while(k && pattern[i+1]==pattern[k]) k=fail[k];
        f[i+1]= pattern[i]==pattern[k]?++k:0;
    }
}

int main() {
    scanf("%s", ori);
    scanf("%s", pattern);
    l1 = strlen(ori);
    l2 = strlen(pattern);
    calc();
    int k=0, i=0;

    while(i<l1){
        if(ori[i]==pattern[k]){
            i++, k++;
            if(k==l2){//匹配完成，匹配下一段字符串
                printf("%d\n", i-k+1);
                i=i-f[k];//f[k]等于 当第k位字符不匹配时，"前面已匹配字符串"的长度
                k=f[k];
            }
        }else{
            if(!k)i++;//连第一位都匹配失败，i移向下一位
            else{
                k=f[k];//跳转
            }
        }
    }
}
```



# 扩展KMP

典型问题：给定串$a,b$，对于$a$的每一个后缀$a_i$，求$a_i$与$b$的最长公共前缀。



## z函数

对于一个长度为$n$的字符串$s$（下标从0开始），定义其z函数，$z[i]$为$s[i:]$与$s$的最大公共前缀长度。

显然有$z[0]=n$

例如：
$$
Z(aabaa)=[n,1,0,2,1]
$$
其朴素$O(n^2)$算法如下

```c++
void calc_z_func(int * z, char * s, int len){
    for(int i=1; i<len; i++){
        z[i] = 0;
        while(i + z[i] < len && s[z[i]] == s[z[i] + i]) z[i]++;
    }
}
```



### 利用z[1]...z[i-1]计算z[i]

定义**匹配段**为 与$s$的某一前缀相同的 $s$的子串。例如$s=aabaa$，则$s[3:]$（"aa"）为一个匹配段。

在计算$z[1]$到$z[i-1]$的过程中，我们记下**最右**（右边界最大的）的匹配段$[l,r]$，该$r$视为算法目前扫描到的边界，任何超过$r$的字符都是**未扫描**的。

下面分情况讨论：

1.  $r\lt i$，由于当前位置处于未扫描的部分，因此使用朴素算法进行扫描匹配即可。

2.  $r\ge i$：

    注意到$s[l\dots r]=s[0\dots (r - l)]$，因此有$s[i\dots r]=s[(i-l)\dots (i-l)+(r-i)]$。因此，我们可以利用$z[i-l]$作为参考。注意到$z[i-l]+i-1$可能超过$r$，而超过$r$的部分都是未扫描的。因此有
    $$
    z[i]=\min(r-i+1,z[i-l])
    $$
    接下来继续使用朴素算法去求就行。

```c++
void calc_z_func(int * z, char * s, int len){
    z[0] = len;
    for(int i=1, l=0, r=0; i<n; i++){
        z[i] = 0;
        if(i <= r) z[i] = min(r - i + 1, z[i-l]);
        while(i + z[i] < len && s[z[i]] == s[z[i] + i]) z[i]++;
        if(i + z[i] - i > r) l = i, r = i + z[i] - 1;
    }
}
```

注意：如果从$i=0$开始，会使得最右匹配段一直为$[0,n-1]$，算法退化为$O(n^2)$



## 求s每个后缀与t的最长公共前缀

在求出上述$z$函数后，仿照$z$函数的求法即可。

$extend[i]$即为后缀$s_i$与$t$的最长公共前缀

```c++
int len_s = strlen(s), len_p = strlen(p);
calc_z_func(p, len_p);

for(int i=0, l = -1, r = -1; i<len_s; i++){
    extend[i] = 0;
    if(r >= i) extend[i] = min(r - i + 1, z[i - l]);
    while(i + extend[i] < len_s && 
          s[i + extend[i]] == p[extend[i]])
         extend[i]++;
    if(extend[i] + i - 1 > r) r = extend[i] + i - 1, l = i;
}
```



## 其他应用

### 查找子串

问题：求串$p$在串$s$中出现的位置

解法：

令$t=p\delta s$，其中$\delta$为$s,p$中均为出现过的字符。

计算$z$函数，对于$i\in\large[\normalsize\mid p\mid+ 1,\mid t\mid - 1\large]$，若$z[i]=\mid p\mid$，则有一个$p$出现在$s$的第$i$号位置。




# 参考链接

我自己的博文：https://blog.csdn.net/Chgtaxihe/article/details/88919673

https://oi-wiki.org/string/z-func/