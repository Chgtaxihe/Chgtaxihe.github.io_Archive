---
layout: hidden_page
title: AC自动机学习笔记
---

* auto-gen TOC:
{:toc}
# 前言

![81Ai9A.png](https://s1.ax1x.com/2020/03/15/81Ai9A.png)



# 参考资料

1.  [强势图解AC自动机](https://www.luogu.com.cn/blog/3383669u/qiang-shi-tu-xie-ac-zi-dong-ji)



# AC自动机

建一个AC自动机分为两步

## 1. 建立一棵Trie树

没有什么要注意的地方。



## 2. 计算fail指针

以下截图来自[参考资料](#参考资料)(1)

![](https://blog.chgtaxihe.top/resource/img/postac_automaton_1.PNG)



```c++
void calc_fail(){
    queue<int> que;
    for(int i=0;i<26;i++) if(child[0][i]) que.push(child[0][i]);

    while(!que.empty()){
        int p = que.front(); que.pop();

        for(int i=0;i<26;i++){
            if(child[p][i]){
                fail[child[p][i]] = child[fail[p]][i];
                que.push(child[p][i]);
            }else{
                child[p][i] = child[fail[p]][i]; //路径压缩
            }
        }
    }
}
```

我们定义根节点为$0$号节点，当新建节点$u$时，$child[u][i]$初始化为$0$（指向根节点）

将子节点依次入队，是为了避免子节点的$fail$指针指向自己

采用$bfs$，当遍历到节点$v$时， 保证深度小于$dep(v)$的节点的$fail$指针已经计算完毕

$fail[child[p][i]] = child[fail[p]][i];$相当于在当前串$p$与$fail[p]$后都有一个字符$i$，当前串匹配失败，则跳转到共同最长后缀处

路径压缩后就避免了$child[fail[k]][i]$不存在，要继续跳$fail[fail[k]]$的情况

