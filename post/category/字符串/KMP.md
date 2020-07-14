---
layout: hidden_page
title: KMP学习笔记
---

* auto-gen TOC:
{:toc}
# 前言

突然发现自己kmp算法掌握得不是很到位。写一篇笔记就当复习好了。



# 定义

$fail[i]$指向的是**当前位失配时，与模式串前缀相同的最长后缀**，也是下一次配对的位置

举个例子，当计算$fail$指针时，假设模式串$pat$为"ababc"

则$fail[]=\{0, 0, 1, 2, 0\}$



# 模板

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
        }
        else{
            if(!k)i++;//连第一位都匹配失败，i移向下一位
            else{
                k=f[k];//跳转
            }
        }
    }
    for(int j=1;j<=l2;j++)printf("%d ", f[j]);
}
```



待补充......