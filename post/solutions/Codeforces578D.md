---
layout: hidden_page
title: Codeforces 578D
---

# Codeforces 578D

出题人给的题解像💩一样



## 非DP做法1

为什么网上的题解都没有给出"**仅**当子串为ababab交替出现时会重复计算"这一解题关键的证明/思路？估计是我太菜了。



对于串$s$，可以把连续相同的字符分在同一组，设组数为$gcnt$。

对于某一个组$g_i$，我们考虑从其中去除一个字符，得到新的字符串$k$，再向其中加入一个字符得到新的串$t\ (t\ne s)$，有$nm- size(g_i)$种。由于向组$g_j(i\ne j)$中任意一个位置添加字符$char(g_j)$得到的串$t$都是相同的，要减去重复计算的数，因此有$ans=nm-size[g_i]+\sum_{j\ne i}size(g_j)=nm-n$

总的答案即为$ans=k(nm-n)$

------

以下证明完全是自找苦吃，还不一定正确

------

下面考虑特殊字符串导致重复计算的情况。

对于一个串$s=...a...b...$，将省略部分分别记为$l、m、r$。

从$s$中分别去掉字符$a、b$得到$k、k'\ (k\ne k')$，然后向$k、k'$中分别添加一个新字符$c_1、c_2$得到$t,t'\ (t\ne r\ \&\ t'\ne r)$，若重复计算，说明$t=t'$，

1.  若$a=b$，则$k=\{lmar\},k'=\{lamr\},k\ne k'$

    1.  （无证明）仅当$m=\{ca\}\ (c\ne a)$循环时$t=t'$

2.  若$a\ne b$，则$k=\{lmbr\},k'=\{lamr\},k\ne k'$

    ​	显然字符$c_1$或$c_2$被添加到$l/r$中时，由于不存在**有限长**的字符串$m$使得$am=mb$（或因为$k\ne k'$），因此定有$t\ne t'$，因此忽略$l、r$，考虑子串$s=a...b$，被省略部分记为$m$。记$k=\{mb\}, k'=\{am\}$。

    ​	同理，当字符被添加进$m$中时，不存在**有限长**的字符串$m=m_1m_2=m_1'm_2'$使得$am_1c_1m_2=m_1'c_2m_2'b$

    1.   若$c_1,c_2\ne a\ \&\ c_1,c_2\ne b$，显然$t\ne t'$
    2.   若$c_1=b,c_2=a$，不存在$m$使$t=t'$
    3.   若$c_1=a, c_2=b$，唯一可行的解为$t=\{mab\},t'=\{abm\}$。易得$m$为$\{ab\}$循环
    4.   若$c_1=c_2$，不存在$m$使$t=t'$

结论：当且仅当字符串$ab$交替出现（ab...a或ab....ab）时会重复计算，且只会被重复计算1次。

最终答案$ans=k(mn-n)-字符交替出现的子串数量$



下面是从大佬那copy来的代码

```c++
#include <cstdio>
#include <cctype>
#define rr register
using namespace std;
int n,m,same; char c1,c2;
signed main(){
    scanf("%d%d",&n,&m);
    while (!isalpha(c1)) c1=getchar();
    rr long long ans=n*(m-1);
    for(rr int i=1;i<n;++i){
        rr char c=getchar();
        same=(c==c2)?same+1:0;
        if(c!=c1) ans+=n*(m-1)-same-1;
        c2=c1; c1=c;
    }
    return !printf("%lld",ans);
} 
```

