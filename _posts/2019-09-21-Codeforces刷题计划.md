---
layout: post
title: Codeforces 刷题计划
tags: algorithm Codeforces
---

# Codeforces 刷题计划~

* auto-gen TOC:
{:toc}
## 说明

有些题目比较简单，就没写题解/AC代码啦

UPD: 我好菜啊



## Div. 1

### Codeforces Round #609 (Div. 1)

[题解](https://codeforces.com/blog/entry/72358)

| 题号                         | 完成 | 备注        | 过题人数 |
| ---------------------------- | ---- | ----------- | -------- |
| D. Invertation in Tournament |      | 我不配 ╥﹏╥ | 93       |
| E. Happy Cactus              |      |             | 58       |



###  Codeforces Round #631 (Div. 1)

| 题号                        | 完成        | 备注                | 过题人数 |
| --------------------------- | ----------- | ------------------- | -------- |
| A. Dreamoon Likes Coloring  | AC(WA14/21) |                     | 1666     |
| B. Dreamoon Likes Sequences | AC(TLE3)    | **记忆化**搜索      | 1735     |
| C. Drazil Likes Heap        | AC          | 贪心+模拟（细节多） | 833      |
| D. Dreamoon Likes Strings   | 题解        |                     | 112      |
| E. Dreamoon Loves AA        |             |                     | 34       |

B题题解

这题不需要搜索

设$h(x)$为$x$的二进制的最高位位置，如$h(1)=0,h(2)=h(3)=1$，那么显然有$h(a_i)<h(a_j)\ (i<j)$

那么对于每一位$v(0\le v\le h(d))$，可以有两类情况：

1.  选：则有$min(2^{v+1}-1,d)-2^v+1$中情况
2.  不选，有1中情况

则该位有$c(v)=min(2^{v+1}-1,d)-2^v+2$种情况

则答案$ans=-1+\prod_{i=0}^{h(d)}c(i)$，之所以要减一是因为要剔除序列长度为0的情况

原理大致同我的dfs搜索一样，但快得多~

------

C题题解

这题正解不是模拟。

<img src="https://s1.ax1x.com/2020/04/13/Gjjj8s.png" alt="Gjjj8s.png" title="Gjjj8s.png" width=800/>

注意：

1.  假设这棵树剩下的元素组成的集合$s$已经确定，那么这棵树的形状就是唯一确定的。

2.  假如一个数$x$不在最终的序列$s$中，那么一定进行过$f(pos_x)$。因此，操作的序列可以由一下方式得出

    ```c++
    bool in_final_set[maxn];
    vector<int> ans;
    for(int i=n; i>=1; i--){
        if(!in_final_set[i]) ans.push_back(i);
    }
    ```

    $ans$即为操作序列

3.  这里有一份更“优雅”的模拟，代码更短，耗时更短(358ms)！

[AC代码](https://codeforces.com/contest/1329/submission/75778994)

------

D题题解

根据题解，最小的操作数为$max(\lceil \frac{\sum c_i}{2} \rceil, max_{0\le i\le25}(c_i)) + 1$

把$s_i=s_{i+1}$的$i$称为`隔板`，可以发现每次操作，如果存在其他不同颜色的隔板，那么我们可以一次消除2个隔板，否则只能一个一个地消。消去所有隔板后，序列仍不为空，还需要一次操作来清空序列，这就是最小操作数式子的由来。



[参考](https://www.cnblogs.com/suwakow/p/12662586.html)（对大佬而言" 思维难度基本上没有 "，o(╥﹏╥)o）



### Codeforces Round #633 (Div. 1)

| 题号                      | 完成    | 备注                          | 过题人数 |
| ------------------------- | ------- | ----------------------------- | -------- |
| A. Powered Addition       | AC(WA3) |                               | 2000     |
| B. Edge Weight Assignment | 题解AC  | 巧妙构造/边权转化为两点权异或 | 1683     |
| C. Perfect Triples        | 题解AC  | 真的是神仙题                  | 1184     |
| D. Nested Rubber Bands    |         |                               | 299      |
| E. JYPnation              |         |                               | 35       |

[B题代码](https://codeforces.com/contest/1338/submission/76771858)

------

C题题解

考虑$[1, 4^n-1]$的数字已经全部使用，那么一定有$a_{2n}=1, a_{2n+1}=0, b_{2n}=0, b_{2n+1}=1$，其中$a_x,b_x$分别代表$a、b$二进制表示的第$x$位

如下图所示

![](https://espresso.codeforces.com/5f0a24543aeade78709e77fee5a18b0e88206748.png)

因而对于$a$的$(i+1,i)(i\in \{0, 2, 4, 6, ...\})$位，有4种取法，每种取法都有唯一对应的$b_{i+1},b_{i},c_{i+1},c_i$，按照这种方法同时可保证把$[1, 4^n-1]$的所有数字用完

![](https://espresso.codeforces.com/0c185d1a6606a7421cc262cc66f2ecdc6d0ada9f.png)

[AC代码](https://codeforces.com/contest/1338/submission/76801718)



###  Codeforces Round #618 (Div. 1) 

| 题号                   | 完成   | 备注                                                        | 过题人数 |
| ---------------------- | ------ | ----------------------------------------------------------- | -------- |
| A. Anu Has a Function) | 题解AC | $(a\mid b)-b=a\&(\sim b)$，注意用`unsigned`和`&与>`的优先级 | 1881     |
| B. Aerodynamic         | 题解AC | 又是一道神仙题                                              | 1403     |
| C. Water Balance       | 题解AC | 差点...                                                     | 1327     |
| D. Around the World    |        |                                                             | 177      |
| E. So Mean             |        |                                                             | 51       |

B题题解

（基本上是翻译）

`Convex Polygon`指`凸多边形`（任意一条边无限延长为直线时，其他各边都在此直线同旁）

如果$\{(x_0,y_0), (0,0)\}\in P(x,y)$，那么$\{(-x_0,-y_0), (0,0)\}\in P(x-x_0,y-y_0)$，因此，$T$中心对称。如果$S\sim T$，必有$S$中心对称。

下面证明`如果S中心对称，则S的每条边放大到原来的2倍后与T全等`

首先平移$S$，使得$S$的对称中心与$(0,0)$重合。

1.  如果$(x_0,y_0)\in P$，那么$\{(0,0),(2x_0,2y_0)\}\in P(x_0,y_0)$
2.  如果$(x_0,y_0)\not\in P$，那么线段$\{(0,0),(x_0,y_0)\}$一定穿过$P$的某一条边$e_0$，下面我们称与$e_0$中心对称的边为$e_0'$。由于$S$是凸多边形，我们把$e_0,e_0'$沿两端无限延长成直线，进而$S$的所有点都夹在$e_0,e_0'$之间，将所有点$(x,y)$放大一倍后，点$(2x_0,2y_0)$定不在新边$e_1,e_1'$范围内。

对称性的判断见代码。

[AC代码](https://codeforces.com/contest/1299/submission/76931783)

------

D题题解

一开始就往斜率的方向考虑， 但是没有发现$a$的什么性质...

看了题解之后，发现可以用前缀和$pre_i$来代替$a_i$，显然如果序列$S$是字典序最小的，那么它对应的前缀和序列也是字典序最小的，反之亦然。又因为$a_i\ge 1$，所以$pre_i$单调递增。

将$x=i,y=pre_i$画出来，考虑进行一次操作$[l,r]$，就相当于使得$p_i=p_{l-1}+\frac{p_r-p_l}{r-l+1}(i-l+1)$，那么要使得$p_i$字典序最小，每次变换都选择一个斜率最小的即可，有点类似斜率dp。

[AC代码](https://codeforces.com/contest/1299/submission/76960393)



###  Codeforces Round #616 (Div. 1) 

| 题号                               | 完成          | 备注                                   | 过题人数 |
| ---------------------------------- | ------------- | -------------------------------------- | -------- |
| A. Mind Control                    | AC            | 想到了暴力，但是没敢做，姑且算自己AC吧 | 1497     |
| B. Irreducible Anagrams            | 题解AC        | 题解的证明很有意思                     | 1251     |
| C. Prefix Enlightenment            | 看题解+代码AC | 2-SAT?不不不                           | 719      |
| D. Coffee Varieties (hard version) |               |                                        | 248      |
| E. Cartesian Tree                  |               |                                        | 64       |
| F. Making Shapes                   |               |                                        | 40       |

[A题AC代码 $O(n^2)$](https://codeforces.com/contest/1290/submission/76987131) 

[A题AC代码 $O(n)$](https://codeforces.com/contest/1290/submission/76996970)

------

C题每个开关只有两个状态，同时一个点$x$最多只会被两个开关$(a,b)$控制，根据$x$的初始状态便可确定$(a,b)$的相对状态（如果$x=off$，则$a,b$有且只有一个被操作，反之$x=on$，$a,b$要么同时操作，要么同时不被操作），对每个开关建两个点，分别代表操作/不操作，并用`dsu`维护联通集，同时维护一个联通集内所需操作数。显然$a_{on},a_{off}$一定是不联通的，那么求答案的时候取一下$min(size[block(a_{on})], size[block(a_{off})])$即可

[C题AC代码](https://codeforces.com/contest/1290/submission/77087660)



### Codeforces Round #614 (Div. 1) 

| 题号                           | 完成         | 备注 | 过题人数 |
| ------------------------------ | ------------ | ---- | -------- |
| A. NEKO's Maze Game            | AC           | 水   | 2138     |
| B. Aroma's Search              | 题解AC(WA49) |      | 1456     |
| C. Xenon's Attack on the Gangs |              |      | 877      |
| D. Chaotic V.                  |              |      | 400      |
| E. Rin and The Unknown Flower  |              |      | 90       |
| F. Nora's Toy Boxes            |              |      | 44       |

[B题AC代码](https://codeforces.com/contest/1292/submission/77541887)



## Div. 2

### Codeforces Round #588 (Div. 2)

[题解](https://codeforces.com/blog/entry/70008) [VirtualJudge](https://vjudge.net/problem#OJId=CodeForces&probNum=1230)

[我的AC代码(C/D/E/F)](https://gist.github.com/Chgtaxihe/3f79063816b1224702acc31e684011aa)

| 题号                             | 完成 | 一句话题解                                                   |
| -------------------------------- | ---- | ------------------------------------------------------------ |
| A. Dawid and Bags of Candies     | √    |                                                              |
| B. Ania and Minimizing           | √    |                                                              |
| C. Anadi and Domino              | √    | 如果n = 7，那么一定有两个点公用一个数字                      |
| D. Marcin and Training Camp      | √    | 如果A和B不是子集关系，那么A比B强且B比A强，$O(n^2)$           |
| E. Kamil and Making a Stream     | √    | AC容易，证明复杂度不易($v$到$v$的祖先路径上的不同的$gcd$不会超过$log(10^12)$个) |
| F. Konrad and Company Evaluation | √    | $ans = \sum OutDegree_i * InDegree_i$ </br>难点在于证明复杂度$O(n + m + q \sqrt{2m})$ |



### Educational Codeforces Round 73

(Virtual Participate)

| 题号                          | 完成 | 一句话题解                                                   | 过题人数 |
| ----------------------------- | ---- | ------------------------------------------------------------ | -------- |
| A. 2048 Game                  | √    |                                                              | 5662     |
| B. Knights                    | √    | 随便猜个结论，居然过了？？？                                 | 4135     |
| C. Perfect Team               | √    |                                                              | 4776     |
| D. Make The Fence Great Again | √    | 每个板子增加的长度不会超过2，故$$dp_{pos, add} = add \cdot b_{pos} + \min\limits_{x=0 \dots 2, a_{pos-1}+x \neq a_{pos}+add} dp_{pos-1, x}$$ | 1426     |
| E. Game With String           | √    | 不容易啊，[题解](https://codeforces.com/blog/entry/69925)    | 122      |
| F. Choose a Square            | ╳    |                                                              | 85       |
| G. Graph And Numbers          | ╳    |                                                              | 12       |



### Codeforces Round #589 (Div. 2)

[题解](https://codeforces.com/blog/entry/70162) [VirtualJudge](https://vjudge.net/problem#OJId=CodeForces&probNum=1228)

[我的AC代码(C/D/E)](https://gist.github.com/Chgtaxihe/0775c7faff399a4fcce0bcac8b203574)

| 题号                         | 完成 | 一句话题解                  | 过题人数 |
| ---------------------------- | ---- | --------------------------- | -------- |
| A. Distinct Digits           | √    |                             | 10912    |
| B. Filling the Grid          | √    | 暴力模拟                    | 6921     |
| C. Primes and Multiplication | √    | 数学太恐怖，去看题解吧      | 4559     |
| D. Complete Tripartite       | √    | 优雅的暴力                  | 2842     |
| E. Another Filling the Grid  | √    | [DP] 题解表述有误，看评论区 | 965      |
| F. One Node is Gone          |      |                             | 209      |



### Educational Codeforces Round 74
[题解](https://codeforces.com/blog/entry/70450)

[我的AC代码(D)](https://gist.github.com/Chgtaxihe/3b2b8526c76d320424d5eb64f939f405)

| 题号                                                         | 完成 | 一句话题解                               | 过题人数 |
| ------------------------------------------------------------ | ---- | ---------------------------------------- | -------- |
| A. [Prime Subtraction](https://codeforces.com/contest/1238/problem/A) | √    |                                          | 6751     |
| B. [Kill `Em All](https://codeforces.com/contest/1238/problem/B) | √    |                                          | 4535     |
| C. [Standard Free2play](https://codeforces.com/contest/1238/problem/C) | √    | 讨论所有1序列的长度                      | 2388     |
| D. [AB-string](https://codeforces.com/contest/1238/problem/D) | √    | 字符串只由AB组成，最后计算的方法也有意思 | 1137     |
| E. [Keyboard Purchase](https://codeforces.com/contest/1238/problem/E) |      |                                          | 263      |
| F. [The Maximum Subtree](https://codeforces.com/contest/1238/problem/F) |      |                                          | 167      |
| G. [Adilbek and the Watering System](https://codeforces.com/contest/1238/problem/G) |      |                                          | 15       |



### Codeforces Round #592 (Div. 2)

[题解](https://codeforces.com/blog/entry/70553)

[我的AC代码(B/C/E)](https://gist.github.com/Chgtaxihe/d18db85859ed76ef8714a01c32728e82)

| 题号                                                         | 完成 | 一句话题解                                                   | 过题人数 |
| ------------------------------------------------------------ | ---- | ------------------------------------------------------------ | -------- |
| A. [Pens and Pencils](https://codeforces.com/contest/1244/problem/A) | √    |                                                              | 10601    |
| B. [Rooms and Staircases](https://codeforces.com/contest/1244/problem/B) | √    | [**贪心**]我好菜                                             | 8449     |
| C. [The Football Season](https://codeforces.com/contest/1244/problem/C) | √    | [**数论**]因为`平局w场 = 赢d场`所以如果有解，定有`平局数 <= w`的解，当然也可以用`exgcd`(Wa了10发) | 3966     |
| D. [Paint the Tree](https://codeforces.com/contest/1244/problem/D) | √    | [图论]比C简单太多了                                          | 3634     |
| E. [Minimizing Difference](https://codeforces.com/contest/1244/problem/E) | √    | [**思维**]最小值/最大值中一个 一定是原序列中的值             | 2432     |
| F. [Chips](https://codeforces.com/contest/1244/problem/F)    |      |                                                              | 799      |
| G. [Running in Pairs](https://codeforces.com/contest/1244/problem/G) |      |                                                              | 764      |



### Codeforces Round #593 (Div. 2)

[题解](https://codeforces.com/blog/entry/70654)

[我的AC代码(C/D)](https://gist.github.com/Chgtaxihe/d2719b1d628446b9221bf99d182fb047)

| 题号                                                         | 完成 | 一句话题解                                      | 通过人数 |
| ------------------------------------------------------------ | ---- | ----------------------------------------------- | -------- |
| A. [Stones](https://codeforces.com/contest/1236/problem/A)   | √    |                                                 | 9451     |
| B. [Alice and the List of Presents](https://codeforces.com/contest/1236/problem/B) | √    | 智障了，没想出来                                | 5826     |
| C. [Labs](https://codeforces.com/contest/1236/problem/C)     | √    | [**贪心**]最优解为$\lfloor\frac{n^2}{2}\rfloor$ | 5886     |
| D. [Alice and the Doll](https://codeforces.com/contest/1236/problem/D) | √    | [**贪心**] + [模拟] 细节巨多                    | 1103     |
| E. [Alice and the Unfair Game](https://codeforces.com/contest/1236/problem/E) |      |                                                 | 331      |
| F. [Alice and the Cactus](https://codeforces.com/contest/1236/problem/F) |      |                                                 | 29       |



### Codeforces Round #594 (Div. 2)

[题解](https://codeforces.com/blog/entry/70720)

[我的AC代码(C)](https://gist.github.com/Chgtaxihe/b7b680cf1157cb4035ffb6330cafbc6f)

| 题号                                                         | 完成 | 一句话题解                                             | 通过人数 |
| ------------------------------------------------------------ | ---- | ------------------------------------------------------ | -------- |
| A. [Integer Points](https://codeforces.com/contest/1248/problem/A) | √    |                                                        | 7454     |
| B. [Grow The Tree](https://codeforces.com/contest/1248/problem/B) | √    | [数学推导] $a^2 + b^2 < (a+1)^2 + (b-1)^2$ $(a \ge b)$ | 7620     |
| C. [Ivan the Fool and the Probability Theory](https://codeforces.com/contest/1248/problem/C) | √    | [**数学**] + [找规律]十分值得做！！！                  | 2760     |
| D1. [The World Is Just a Programming Task (Easy Version)](https://codeforces.com/contest/1248/problem/D1) |      |                                                        | 1262     |
| D2. [The World Is Just a Programming Task (Hard Version)](https://codeforces.com/contest/1248/problem/D2) |      |                                                        | 197      |
| E. [Queue in the Train](https://codeforces.com/contest/1248/problem/E) |      |                                                        | 231      |
| F. [Catowice City](https://codeforces.com/contest/1248/problem/F) |      |                                                        | 252      |



### Educational Codeforces Round 75 (Rated for Div. 2)

[题解](https://codeforces.com/blog/entry/70860)

[我的AC代码(C/D)](https://gist.github.com/Chgtaxihe/f36f4e226d76a8467ae2f3e2867b1872)

| 题号                                                         | 完成 | 一句话题解                                           | 通过人数 |
| ------------------------------------------------------------ | ---- | ---------------------------------------------------- | -------- |
| A. [Broken Keyboard](https://codeforces.com/contest/1251/problem/A) | √    |                                                      | 5994     |
| B. [Binary Palindromes](https://codeforces.com/contest/1251/problem/B) | √    | [**找规律**]观察                                     | 3640     |
| C. [Minimize The Integer](https://codeforces.com/contest/1251/problem/C) | √    | [贪心]                                               | 2632     |
| D. [Salary Changing](https://codeforces.com/contest/1251/problem/D) | √    | 想到思路敲不出来，那么不妨用暴力简化一下Coding复杂度 | 985      |
| E1. [Voting (Easy Version)](https://codeforces.com/contest/1251/problem/E1) |      |                                                      | 227      |
| E2. [Voting (Hard Version)](https://codeforces.com/contest/1251/problem/E2) |      |                                                      | 181      |
| F. [Red-White Fence](https://codeforces.com/contest/1251/problem/F) |      |                                                      | 28       |



### Codeforces Round #597 (Div. 2)

[题解](https://codeforces.com/blog/entry/71080)

[我的AC代码(D)](https://gist.github.com/Chgtaxihe/01f925fe7ae09ad6a586d76b8b706af4)

| 题号                                                         | 完成 | 一句话题解                                                   | 通过人数 |
| ------------------------------------------------------------ | ---- | ------------------------------------------------------------ | -------- |
| A. [Good ol' Numbers Coloring](https://codeforces.com/contest/1245/problem/A) | √    | [**数学**] 转化成数学式子，如`a + b`一定是白色的.结论: 如果$gcd(a, b) = 1$ 则  `x`是`白色`的 $(x>a*b)$,否则定存在 $x \bmod gcd(a,b) \neq 0$ 使得 $ax+by\neq x$ | 8460     |
| B. [Restricted RPS](https://codeforces.com/contest/1245/problem/B) | √    | 题目很简单，但是比较考代码功底，基础差一点的写出来的代码就是乱七八糟(结果正确，只不过实现得很难看而已) | 6982     |
| C. [Constanze's Machine](https://codeforces.com/contest/1245/problem/C) | √    | 显而易见的DP题                                               | 6241     |
| D. [Shichikuji and Power Grid](https://codeforces.com/contest/1245/problem/D) | √    | 想到了方法但是敲不出来，往往是因为思路混乱，又或是做法未经简化。两种做法: </br> 1. 设计一个代价函数$C(u, v)$来跑最小生成树  </br> 2. 与其建一个森林(图论)，不如引入一个`新的点`将森林的根连接起来，然后最小生成树 | 2852     |
| E. [Hyakugoku and Ladders](https://codeforces.com/contest/1245/problem/E) |      |                                                              | 680      |
| F. [Daniel and Spring Cleaning](https://codeforces.com/contest/1245/problem/F) |      |                                                              | 886      |



###  Codeforces Round #599 (Div. 2) 

[题解](https://codeforces.com/blog/entry/71216)

[我的AC代码](https://gist.github.com/Chgtaxihe/2b93232260a14cb2706e93aece4a2077)

| 题号                                                         | 完成 | 一句话题解            | 通过人数 |
| ------------------------------------------------------------ | ---- | --------------------- | -------- |
| A. [Maximum Square](https://codeforces.com/contest/1243/problem/A) | √    | 排序                  | 9682     |
| B1. [Character Swap (Easy Version)](https://codeforces.com/contest/1243/problem/B1) | √    | 分类讨论              | 8321     |
| B2. [Character Swap (Hard Version)](https://codeforces.com/contest/1243/problem/B2) | √    | 看代码/题解吧         | 3932     |
| C. [Tile Painting](https://codeforces.com/contest/1243/problem/C) | √    | [**数论**]见下        | 5258     |
| D. [0-1 MST](https://codeforces.com/contest/1243/problem/D)  | √    | 正确估计复杂度 + 实现 | 1754     |
| E. [Sum Balance](https://codeforces.com/contest/1243/problem/E) |      |                       | 198      |

C题题解

对于$n=p^k$(p为质数)，有$ans = p$ (A)

对于$n = pq$ ($gcd(p, q) = 1$)，有$ans=1$ (B)

下面对(B)进行证明

对于任意$i$和$j(i\neq j)$，存在$1 \le x \le n$使得$x \equiv i \pmod{p}$且$x \equiv j \pmod{q}$(中国剩余定理)

因此$i$和$j(i\neq j)$颜色与$x$相同

------

D题题解

暴力即可(set/bitset记录连通块)



### Educational Codeforces Round 76 (Rated for Div. 2)

[题解](https://codeforces.com/blog/entry/71434)

[我的AC代码](https://gist.github.com/Chgtaxihe/3abf4c039992ed9a37ae8cc9613e650e)

| 题号                                                         | 完成 | 一句话题解                                                   | 通过人数 |
| ------------------------------------------------------------ | ---- | ------------------------------------------------------------ | -------- |
| A. [Two Rival Students](https://codeforces.com/contest/1257/problem/A) | √    |                                                              | 7551     |
| B. [Magic Stick](https://codeforces.com/contest/1257/problem/B) | √    |                                                              | 6573     |
| C. [Dominated Subarray](https://codeforces.com/contest/1257/problem/C) | √    | 贪心                                                         | 5177     |
| D. [Yet Another Monster Killing Problem](https://codeforces.com/contest/1257/problem/D) | √    | [**思维**]需要注意到$1\leq s \leq n$(BTW, 用Python AC的代码基本都是压着时限卡过去的) | 1728     |
| E. [The Contest](https://codeforces.com/contest/1257/problem/E) |      |                                                              | 748      |
| F. [Make Them Similar](https://codeforces.com/contest/1257/problem/F) |      |                                                              | 142      |
| G. [Divisor Set](https://codeforces.com/contest/1257/problem/G) |      |                                                              | 34       |



### Codeforces Round #600 (Div. 2)

[题解](https://codeforces.com/blog/entry/71489)

[我的AC代码](https://gist.github.com/Chgtaxihe/49e435d6745c431b3be45412230c2113)

| 题号                                                         | 完成 | 备注                             | 通过人数 |
| ------------------------------------------------------------ | ---- | -------------------------------- | -------- |
| A. [Single Push](https://codeforces.com/contest/1253/problem/A) | √    |                                  | 8804     |
| B. [Silly Mistake](https://codeforces.com/contest/1253/problem/B) | √    |                                  | 5743     |
| C. [Sweets Eating](https://codeforces.com/contest/1253/problem/C) | √    |                                  | 5690     |
| D. [Harmonious Graph](https://codeforces.com/contest/1253/problem/D) | √    | 题解的思路比我的更简单易懂(更优) | 4046     |
| E. [Antenna Coverage](https://codeforces.com/contest/1253/problem/E) | √    | [**Dp**]                         | 1464     |
| F. [Cheap Robot](https://codeforces.com/contest/1253/problem/F) |      |                                  | 520      |



### Codeforces Round #601 (Div. 2)

[题解](https://codeforces.com/blog/entry/71594)

[我的AC代码](https://gist.github.com/Chgtaxihe/6cae819ea8ccc42ba7a13bd74cd950d7)

| 题号                                                         | 完成 | 备注                                                         | 通过人数 |
| ------------------------------------------------------------ | ---- | ------------------------------------------------------------ | -------- |
| A. [Changing Volume](https://codeforces.com/contest/1255/problem/A) | √    |                                                              | 9713     |
| B. [Fridge Lockers](https://codeforces.com/contest/1255/problem/B) | √    |                                                              | 6467     |
| C. [League of Leesins](https://codeforces.com/contest/1255/problem/C) | √    |                                                              | 3659     |
| D. [Feeding Chicken](https://codeforces.com/contest/1255/problem/D) | √    | python3的builtdins.input()比pypy3的快                        | 1842     |
| E1. [Send Boxes to Alice (Easy Version)](https://codeforces.com/contest/1255/problem/E1) | √    |                                                              | 1213     |
| E2. [Send Boxes to Alice (Hard Version)](https://codeforces.com/contest/1255/problem/E2) | √    | 对$a$求前缀和$S_i$，那么$box_i$向$box_{i+1}$移动一块，相当于$S_i -= 1$，对于$factor_k$,使得$all(S_i\%factor_k=0)$即可 | 604      |
| F. [Point Ordering](https://codeforces.com/contest/1255/problem/F) |      |                                                              | 142      |



###  Educational Codeforces Round 77 (Rated for Div. 2)

[题解](https://codeforces.com/blog/entry/71805)

[我的AC代码](https://gist.github.com/Chgtaxihe/51c3fb94efd178b1f0fe2e408548777e)

| 题号                                                         | 完成 | 备注                                                         | 通过人数 |
| ------------------------------------------------------------ | ---- | ------------------------------------------------------------ | -------- |
| A. [Heating](https://codeforces.com/contest/1260/problem/A)  | √    |                                                              | 5450     |
| B. [Obtain Two Zeroes](https://codeforces.com/contest/1260/problem/B) | √    | 对于$(a+b)\equiv0\pmod{3}$,定有$2a\equiv b\pmod3$(枚举一下$a$和$b$即可证明)故本题只需要满足$(a+b)\equiv 0\pmod3$和$min(a,b)*2\ge max(a,b)$即可 | 4380     |
| C. [Infinite Fence](https://codeforces.com/contest/1260/problem/C) | √    |                                                              | 2075     |
| D. [A Game with Traps](https://codeforces.com/contest/1260/problem/D) | √    | 注意到：对与一个要排除的陷阱$(l_k, r_k, d_k)$，若$l_k <= r_k$，则我们需要经过区域$[l_k, r_k]$三次（人生苦短，我用C++） | 796      |
| E. [Tournament](https://codeforces.com/contest/1260/problem/E) |      |                                                              | 194      |
| F. [Colored Tree](https://codeforces.com/contest/1260/problem/F) |      |                                                              | 20       |

C题题解

假定$r\le b$， $g=gcd(r, b)$，存在$rx - by = g$ ($y\ge0$)，即$rx = g + by$ ($y\ge0$)

则对于两个相邻的蓝色块$by$与$by + b$，我们要在其中插入$m+1$个红色块，

$by+g, by+g+r, by+g+2r,...,by+g+(m*r)$

且 $by+g+(m*r) < by+b$

也就是说$m+1 \ge k$，即$g + (k-1)*r < b$ 时`REBEL`，否则`OBEY`



### Codeforces Round #603 (Div. 2)

[题解](https://codeforces.com/blog/entry/71844?locale=en)

[我的AC代码](https://gist.github.com/Chgtaxihe/3056e723c8e312749fe62e6a8c7d61e9)

| 题号                                                         | 完成 | 备注                                                         | 通过人数 |
| ------------------------------------------------------------ | ---- | ------------------------------------------------------------ | -------- |
| A. [Sweet Problem](https://codeforces.com/contest/1263/problem/A) | √    | 若$a\ge b\ge c$且$a \le b+c$，则按照最优策略，最后剩下的总糖果数为`0`或`1` | 8681     |
| B. [PIN Codes](https://codeforces.com/contest/1263/problem/B) | √    |                                                              | 5919     |
| C. [Everyone is a Winner!](https://codeforces.com/contest/1263/problem/C) | √    | 所有$k = \lfloor \sqrt{n} \rfloor$都属于是答案的一部分       | 6194     |
| D. [Secret Passwords](https://codeforces.com/contest/1263/problem/D) | √    |                                                              | 5144     |
| E. [Editor](https://codeforces.com/contest/1263/problem/E)   | √    | 第一反应是线段树，题解用两个`stack`维护左右两侧信息          | 1629     |
| F. [Economic Difficulties](https://codeforces.com/contest/1263/problem/F) |      |                                                              | 448      |

F题题解

以`cursor`为界，分为左右两部分。同时计算左侧前缀和、右侧后缀和("("计1，")"计-1)。

若左侧合法，则定有$min(sum_{left}) \ge 0$，右侧合法则定有$max(sum_{right}) \le 0$

若整个串合法，除上述条件外，$sum_{left} + sum_{right}=0$

那么最大深度为$max(sum_{left}, max(sum_{left}), -min(sum_{right}))$

复杂度$O( n )$



### Codeforces Round #604 (Div. 2)

[题解](https://codeforces.com/blog/entry/71995)

[我的AC代码](https://gist.github.com/Chgtaxihe/086b10066ac0b4c1fa9c5f3a274d376b)

| 题号                                                         | 完成 | 备注                                                         | 通过人数 |
| ------------------------------------------------------------ | ---- | ------------------------------------------------------------ | -------- |
| A. [Beautiful String](https://codeforces.com/contest/1265/problem/A) | √    |                                                              | 8368     |
| B. [Beautiful Numbers](https://codeforces.com/contest/1265/problem/B) | √    |                                                              | 6432     |
| C. [Beautiful Regional Contest](https://codeforces.com/contest/1265/problem/C) | √    |                                                              | 4708     |
| D. [Beautiful Sequence](https://codeforces.com/contest/1265/problem/D) | √    | 需要注意的是，尽管$cnt[min] < cnt[min+1]$，但$min$仍可能放在开头位置，样例"20000 39999 20000 0" | 2331     |
| E. [Beautiful Mirrors](https://codeforces.com/contest/1265/problem/E) | √    | 复习了一下概率dp和逆元~                                      | 1261     |
| F. [Beautiful Bracket Sequence (easy version)](https://codeforces.com/contest/1265/problem/F) | X    | 没懂！！                                                     | 134      |

E题题解

没什么好说的，概率dp

$cost_i = cost_{i-1} + 1 + (1-p_i)cost_i$

------

F题待完成！！！



### Codeforces Round #607 (Div. 2)

[题解](https://codeforces.com/blog/entry/72212)

[我的AC代码](https://gist.github.com/Chgtaxihe/e88cbaa483f8bb0d1895406ebc5d9e5e)

| 题号                                                         | 完成 | 备注                                                         | 通过人数 |
| ------------------------------------------------------------ | ---- | ------------------------------------------------------------ | -------- |
| A. [Suffix Three](https://codeforces.com/contest/1281/problem/A) | √    |                                                              | 8724     |
| B. [Azamon Web Services](https://codeforces.com/contest/1281/problem/B) | √    | 找到**可交换**且字典序最小的字符a，若有多个a，取pos**最大**的那个 **BTW**：题解给出的代码挺巧妙的 | 3864     |
| C. [Cut and Paste](https://codeforces.com/contest/1281/problem/C) | √    | 看了一眼题解，原来直接把前`x`个字符记录下来并保存到`vector`里也能过(935ms, $O(|S| + x)$), 那怎么我不偷鸡的递归查找就不能过了呢？(用记忆化搜索后时间降到62ms，复杂度$O(\log x)$ ) 另外，用`std::string`拼接更快，很迷，估计是是我想复杂了 | 1656     |
| D. [Beingawesomeism](https://codeforces.com/contest/1281/problem/D) | √    | 分类讨论                                                     | 1115     |
| E. [Jeremy Bearimy](https://codeforces.com/contest/1281/problem/E) | √    | 看题解！！！！                                               | 293      |
| F. [Miss Punyverse](https://codeforces.com/contest/1281/problem/F) |      |                                                              | 30       |



### Codeforces Round #608 (Div. 2)

[题解](https://codeforces.com/blog/entry/72247)

[我的AC代码](https://gist.github.com/Chgtaxihe/78f2b80c0d926f72a220436ccf821986)

| 题号                                                         | 完成 | 备注                                                         | 通过人数 |
| ------------------------------------------------------------ | ---- | ------------------------------------------------------------ | -------- |
| A. [Suits](https://codeforces.com/contest/1271/problem/A)    | √    |                                                              | 8738     |
| B. [Blocks](https://codeforces.com/contest/1271/problem/B)   | √    |                                                              | 5835     |
| C. [Shawarma Tent](https://codeforces.com/contest/1271/problem/C) | √    |                                                              | 5611     |
| D. [Portals](https://codeforces.com/contest/1271/problem/D)  | √    | 做不到全局最优，只能局部最优+dp。题解说还可以维护一个`undoable list`当士兵不够的时候就`undo`，感觉可以用优先队列做 | 1168     |
| E. [Common Number](https://codeforces.com/contest/1271/problem/E) | √    | 有点像二叉树，看题解吧                                       | 1538     |
| F. [Divide The Students](https://codeforces.com/contest/1271/problem/F) | √    | dfs剪枝                                                      | 77       |



### Educational Codeforces Round 78 (Rated for Div. 2)

[题解](https://codeforces.com/blog/entry/72330)

[我的AC代码](https://gist.github.com/Chgtaxihe/ddd4e73649fd8555d82224561e94c324)

| 题号                                                         | 完成 | 备注                                             | 通过人数 |
| ------------------------------------------------------------ | ---- | ------------------------------------------------ | -------- |
| A. [Shuffle Hashing](https://codeforces.com/contest/1278/problem/A) | √    |                                                  | 5820     |
| B. [A and B](https://codeforces.com/contest/1278/problem/B)  | √    | [**数学**]看一波题解                             | 3270     |
| C. [Berry Jam](https://codeforces.com/contest/1278/problem/C) | √    | 比B简单                                          | 1996     |
| D. [Segment Tree](https://codeforces.com/contest/1278/problem/D) | √    | [**优化**]                                       | 514      |
| E. [Tests for problem D](https://codeforces.com/contest/1278/problem/E) | √    | [**贪心**]差分约束了半天出不了结果，还是看题解吧 | 291      |
| F. [Cards](https://codeforces.com/contest/1278/problem/F)    |      |                                                  | 73       |



### Codeforces Round #609 (Div. 2)

[我的AC代码](https://gist.github.com/Chgtaxihe/ca4af5c0f847fab5f4589e00648b395d)

| 题号                      | 完成 | 备注                                                         | 通过人数 |
| ------------------------- | ---- | ------------------------------------------------------------ | -------- |
| A. Equation               | √    |                                                              | 9859     |
| B. Modulo Equality        | √    | 这题用dict/map做，代码量会少一点                             | 5103     |
| C. Long Beautiful Integer | √    | 脑子没转过来，漏判一个条件~怎么回事??????                    | 3471     |
| D. Domino for Young       | √    | [**思维**]如果把图按棋盘的方式涂色，那么一个`domino`永远会占用一黑一白两种颜色的格子 | 1945     |
| E. K Integers             | √    | 看不懂题解。。估计是我境界不够                               | 253      |

E题题解

题解讲的不是很清楚，这里做一下记录

首先，对于一个定值$k$，我们来讨论一下如何求解:

首先计算原序列中`1 - k`中的逆序对数为$inv$， 接下来我们改变一下原序列

`arr = [1 if x <= k else 0 for x in arr]`

这样任务就变成了计算产生$k$个连续的1所需的操作步数，显然只需要把所有数字移动到中位即可



那么对于$1 \le k \le n$，只需用一个树状数组维护逆序对和中位，并将$k$从1遍历到$n$即可求出答案。

（统计答案时可以用树状数组计算前缀和，因此代码中一共了两个树状数组）



### Codeforces Round #610 (Div. 2)

[我的AC代码](https://gist.github.com/Chgtaxihe/b89358bd1628631bdcd5a9a33537a24a)

| 题号                                      | 完成 | 备注                                     | 通过人数 |
| ----------------------------------------- | ---- | ---------------------------------------- | -------- |
| A. Temporarily unavailable                | √    |                                          | 9204     |
| B1. K for the Price of One (Easy Version) | √    | [贪心]                                   | 6128     |
| B2. K for the Price of One (Hard Version) | √    | [贪心]                                   | 5059     |
| C. Petya and Exam                         | √    | [**贪心**]在$t_i - 1$时刻离开是最佳的    | 2532     |
| D. Enchanted Artifact                     | √    | [**思维**]关键在于如何求出`a`和`b`的数量 | 1255     |
| E. The Cake Is a Lie                      |      |                                          | 595      |



### Educational Codeforces Round 79 (Rated for Div. 2)

[我的AC代码](https://gist.github.com/Chgtaxihe/d86643d5f6fb1634e359df0df973057e)

| 题号                          | 完成 | 备注                                                         | 通过人数 |
| ----------------------------- | ---- | ------------------------------------------------------------ | -------- |
| A. New Year Garland           | √    |                                                              | 6821     |
| B. Verse For Santa            | √    | **如果只能背到第x段，那么跳过大于x的段落是没用的！**不然就WA | 4492     |
| C. Stack of Presents          | √    |                                                              | 3687     |
| D. Santa's Bot                | √    | 除了A之外最简单的一题？                                      | 1672     |
| E. New Year Permutations      |      | 感觉可以做，但是过题人数有点恐怖                             | 32       |
| F. New Year and Handle Change |      |                                                              | 36       |



###  Codeforces Round #630 (Div. 2)

两个号都上1600，再也不能打Div3了 <img src="https://s1.ax1x.com/2020/03/28/GAPit0.png" alt="GAPit0.png" title="GAPit0.png" width=150/>

| 题号                   | 完成    | 备注                    | 通过人数 |
| ---------------------- | ------- | ----------------------- | -------- |
| A. Exercising Walk     | 赛时-AC |                         | 9009     |
| B. Composite Coloring  | 赛时-AC | 第11个质数:31,第12个:37 | 5767     |
| C. K-Complete Word     | 赛时-AC |                         | 5066     |
| D. Walk on Matrix      | 赛时-AC |                         | 3046     |
| E. Height All the Same | AC      |                         | 783      |
| F. Independent Set     |         |                         | 142      |
| G. No Monotone Triples |         |                         | 11       |

E题题解

在完成分类讨论之后，这道题有两个入手点（已知$nm$为偶数）

1.  $(O+E)^{mn}=\sum_{i=0}^{nm/2} C_{nm}^{2i}O^{2i}E^{nm-2i} + \sum_{i=1}^{nm/2}C_{nm}^{2i-1}O^{2i-1}E^{nm-2i+1}$

    $(O-E)^{mn}=\sum_{i=0}^{nm/2} C_{nm}^{2i}O^{2i}E^{nm-2i} - \sum_{i=1}^{nm/2}C_{nm}^{2i-1}O^{2i-1}E^{nm-2i+1}$

    两式相加除以2即为结果

2.  大神解法，目前还无法理解

    ![](https://blog.chgtaxihe.top/resource/img/post/Codeforces刷题计划_1.PNG)

3.  使用矩阵乘法：考虑$dp_{odd}[i]$代表$i$个格子中有奇数个奇数格的选法，$dp_{even}[i]$代表$i$个格子中有偶数个奇数格的选法，那么有

    $dp_{odd}[i] = dp_{odd}[i-1] \cdot E + dp_{even}[i-1] \cdot O$

    $dp_{even}[i] = dp_{even}[i-1] \cdot E + dp_{odd}[i-1] \cdot O$

    显然可以转化为矩阵乘法，矩阵快速幂可解！
    
    [AC代码](./post/category/动态规划/广义矩阵乘法.html)



###  Codeforces Round #635 (Div. 2) 

改名叫Queueforces得了

| 题号                          | 完成        | 备注   | 通过人数 |
| ----------------------------- | ----------- | ------ | -------- |
| A. Ichihime and Triangle      | AC          |        | 17784    |
| B. Kana and Dragon Quest game | AC          |        | 17336    |
| C. Linova and Kingdom         | 题解AC(WA6) |        | 7213     |
| D. Xenia and Colorful Gems    | 题解AC      |        | 4646     |
| E. Kaavi and Magic Spell      | 题解AC      | Dp     | 641      |
| F. Yui and Mahjong Set        |             | 交互题 | 46       |

[D题AC代码](https://codeforces.com/contest/1337/submission/77932688)

------

E题：$dp[i][j]$表示已经使用了$i$个字符，得到的$A$仍需往头部添加$j$个字符才能构成前缀$T$时，有多少种可能

[E题AC代码(题解我都写到注释里了)](https://codeforces.com/contest/1337/submission/78343453)



###  Codeforces Round #637 (Div. 2) 

| 题号 | 完成 | 备注 | 通过人数 |
| ---- | ---- | ---- | -------- |
| A. Nastya and Rice  | AC |      | 16039 |
| B. Nastya and Door  | AC(3WA2/RE3) |      | 11885 |
| C. Nastya and Strange Generator  | AC | 有点麻烦，其实可以转化成求序列是否由数段连续上升序列组成 | 7929 |
| D. Nastya and Scoreboard  | 题解AC |      | 3195 |
| E. Nastya and Unexpected Guest  | 题解AC | 01BFS: 边权为0则放到队首，边权为1放到队尾 | 313 |
| F. Nastya and Time Machine  |      |      | 57 |

D题题解：

一直想着用$dp[i][j]$来表示前$i$个数字操作了$j$次时能表示的最大数字，结果被复杂度被卡死在$O(2nklog_2k)=O(8e7)$(因为要排序并离散化)

题解给的是：$dp[i][j]$表示后$i$个数字操作了$j$次时是否合法($true$或$false$)，那么只要从$dp[n][k]$贪心的往前回溯即可得到最优解，复杂度$O(10nk)=O(4e7)$

PS: 4e7能过，说不定8e7也能过？

[AC代码](https://codeforces.com/contest/1341/submission/78402343)，代码中$dp[i][j]$的含义与上述$dp$略微不同

------

E题题解：

如果在$T_i$到达了某个点$v$，令$T_i \equiv j \mod{G}$，那么对于任意时刻$T_j(T_j>T_i\ \&\ T_j\equiv T_i\mod G)$，都不应当到达该点$v$，否则发生循环（浪费时间）。因为$G\le 1000$，我们让每个点对应$G$个新图上的点$V_{ij}$，跑01BFS即可。

[AC代码](https://codefoces.com/contest/1341/submission/78467270)，代码中有01dfs的解析

另：大佬的另一种思路

![](https://blog.chgtaxihe.top/resource/img/post/Codeforces刷题计划_2.PNG)

[大佬的AC代码](https://codeforces.com/contest/1340/submission/77903961)



###  Educational Codeforces Round 86

| 题号 | 完成 | 备注 | 通过人数 |
| ---- | ---- | ---- | -------- |
| A. Road To Zero  | AC(3WA2/1WA1) | 1. inf不够大 2. 没看到x,y>0 | 12855 |
| B. Binary Period  | AC |      | 11321 |
| C. Yet Another Counting Problem  | 题解AC |      | 3934 |
| D. Multiple Testcases  | 题解AC |      | 1676 |
| E. Placing Rooks  | 题解AC | 容斥 | 313 |
| F. Make It Ascending  |      |      | 19 |

C题题解:

$(ab+x)\mod a \mod b=x\mod a\mod b$，且$(ab+x)\mod b \mod a=x\mod b\mod a$

可以看出循环节大小为$ab$

[AC代码](https://codeforces.com/contest/1342/submission/78530939)

------

D题题解：

设$cnt_i$为大于等于$i$的数组个数，那么所需的最小testcase数为$ans=max(\lceil \frac{cnt_i}{c_i} \rceil)$。

接着把$m$从小到大/从大到小排序，第$i$个数装进第$i\mod ans$个testcase中。

[AC代码](https://codeforces.com/contest/1342/submission/78547809)

------

E题题解：

由于只有$n$块石头，因而可以每行（或每列）有且只有一块石头，考虑每行一块的情况，结果乘2（除非k=0，此时每行与每列都满足"有且只有一块石头"）即可。

由观察可发现，问题可转化为：把$n$块石头，分到$n-k$列，使得每列至少有一块，共有多少种分法。

首先任选$n-k$列，有$C_n^{n-k}$种选法，下面考虑如何把$n$块石头分到$c$列中

根据容斥原理，首先每块石头有$c$种选择（不同行的石头不等价），即$c^n$，减去单列为空的情况$C_c^1(c-1)^n$，补上两列为空的$C_c^2(c-2)^n$，再减去三列为空的$C_c^3(c-3)^n$，以此类推，得到公式$ans=\sum_{i=0}^c(-1)^iC_c^i(c-i)^n$

![](https://blog.chgtaxihe.top/resource/img/post/Codeforces刷题计划_3.PNG)

[AC代码](https://codeforces.com/contest/1342/submission/78582537)

PS：容斥原理：$\mid\large\cup_{i=1}^nA_i\mid=\sum_{C\subseteq B}(-1)^{size(C)-1}\mid\large\cap_{e\in C}e\mid$

PS2: 事实上，上述的$ans$即为第二类斯特林数$S(n, c)$乘上$c!$（因为不同的行之间不等价）



###  Codeforces Round #647 (Div. 2) 

| 题号 | 完成 | 备注 | 通过人数 |
| ---- | ---- | ---- | -------- |
| A. Johnny and Ancient Computer  | AC(WA2) |      | 13351 |
| B. Johnny and His Hobbies  | AC(2WA2) |      | 10803 |
| C. Johnny and Another Rating Drop  | AC |      | 9480 |
| D. Johnny and Contribution  | AC |  | 3695 |
| E. Johnny and Grandmaster  | 题解 | 很棒的[题解](https://www.youtube.com/watch?v=ZPQzYDf5A4Y)（与出题者思路不同） | 687 |
| F. Johnny and Megan's Necklace  |      |      | 59 |



### Codeforces Round #648 (Div. 2)

心态炸了，A题这么简单都没过，~~不知得掉多少分~~

*UPD:1631$\to$1630* 

| 题号 | 完成         | 备注 | 通过人数 |
| ---- | ------------ | ---- | -------- |
| A. Matrix Game  | 赛后AC(4WA2) | 一开始看错了题，然而后来还是没过... | 13357 |
| B. Trouble Sort   | AC |      | 11706 |
| C. Rotation Matching   | AC |      | 10021 |
| D. Solve The Maze | 赛后AC(2WA7) | 一个变量名写错了，愣是没做出来（居然Wa7，我也是服了） | 6152 |
| E. Maximum Subsequence Value   | AC(2WA6,WA3) | 没有仔细分析：子序列的元素个数不会超过3（离比赛结束还有30s的时候才AC） | 3837 |
| F. Swaps Again   | 题解AC(WA119) |      | 1946 |
| G. Secure Password   | 题解AC | 很有意思的解法 | 211 |

------

>   If we consider the unordered pair of elements $\{ai,an−i+1\}$, then after any operation, the multiset of these pairs (irrespective of the ordering of elements within the pair) stays the same! 

[F题AC代码](https://codeforces.com/contest/1365/submission/83152736)

关键在于找到通过B构造出A的方法。

------

相关知识: Sperner's theorem

E题通过编码方式，使得任意两个编码互不为子集，进而查询时只需查询该位为1的OR。

[E题AC代码(看标程前)](https://codeforces.com/contest/1365/submission/83184135)

[E题AC代码(看标程后)](https://codeforces.com/contest/1365/submission/83184363)



###  Codeforces Round #646 (Div. 2) 

| 题号 | 完成 | 备注 | 通过人数 |
| ---- | ---- | ---- | -------- |
| A. Odd Selection  | AC(WA3) |      | 16056 |
| B. Subsequence Hate  |      |      | 11592 |
| C. Game On Leaves  |      |      | 9145 |
| D. Guess The Maximums  |      |      | 2519 |
| E. Tree Shuffling  |      |      | 3769 |
| F. Rotating Substrings  |      |      | 525 |




## Div. 3

### Codeforces Round #587 (Div. 3)

[我的AC代码(C/E2/F)](https://gist.github.com/Chgtaxihe/7a268e89d6d5913ef37a8948d7f7c6b2)

| 题号                                  | 完成 | 一句话题解 | 通过人数 |
| ------------------------------------- | ---- | ---------- | -------- |
| A. Prefixes                           | √    | Water      | 5931     |
| B. Shooting                           | √    |            | 5577     |
| C. White Sheet                        | √    | 有点小麻烦 | 1331     |
| D. Swords                             | √    |            | 3388     |
| E1. Numerical Sequence (easy version) | √    |            | 670      |
| E2. Numerical Sequence (hard version) | √    | 不容易啊   | 128      |
| F. Wi-Fi                              | √    | DP好难     | 185      |



### Codeforces Round #590 (Div. 3)

[我的AC代码(B2/D/E/F)](https://gist.github.com/Chgtaxihe/77b664c4c8a4295140c6310a23b218e2)

| 题号                              | 完成 | 一句话题解                                                   | 通过人数 |
| --------------------------------- | ---- | ------------------------------------------------------------ | -------- |
| A. Equalize Prices Again          | √    |                                                              | 8366     |
| B1. Social Network (easy version) | √    |                                                              | 6851     |
| B2. Social Network (hard version) | √    | 我服了，出题人专门出了一组数据来Hack unordered_set，用set即或[自定义hash](https://codeforces.com/blog/entry/62393) | 4712     |
| C. Pipes                          | √    |                                                              | 2924     |
| D. Distinct Characters Queries    | √    | 看题解半天都看不懂，才发现是读错题了                         | 2035     |
| E. Special Permutations           | √    |                                                              | 455      |
| F. Yet Another Substring Reverse  | √    | 感觉这题比F简单，刚开始还以为是水过的（毕竟DFS），后来发现只要把DFS改成一个for就是正解了 | 151      |



### Codeforces Round #595 (Div. 3)

[我的AC代码(F题)](https://gist.github.com/Chgtaxihe/83ff3d95037537d11a3d9cbe51020b11)

| 题号                                 | 完成 | 一句话题解                                                   | 通过人数 |
| ------------------------------------ | ---- | ------------------------------------------------------------ | -------- |
| A. Yet Another Dividing into Teams   | √    |                                                              | 8354     |
| B1. Books Exchange (easy version)    | √    |                                                              | 7001     |
| B2. Books Exchange (hard version)    | √    |                                                              | 4520     |
| C1. Good Numbers (easy version)      | √    |                                                              | 4500     |
| C2. Good Numbers (hard version)      | √    |                                                              | 2785     |
| D1. Too Many Segments (easy version) | √    |                                                              | 893      |
| D2. Too Many Segments (hard version) | √    |                                                              | 726      |
| E. By Elevator or Stairs?            | √    |                                                              | 1483     |
| F. Maximum Weight Subset             | √    | [**树Dp**] `dp[u][dep]`代表以`u`为根的子树中，被选取的点深度至少为`dep`时最大的`weight`之和 | 152      |



### Codeforces Round #598 (Div. 3)

[我的AC代码（C/D/E/F）](https://gist.github.com/Chgtaxihe/609ee28d9f9e40b2dc7cad4f54c08ec7)

| 题号                               | 完成 | 一句话题解                                                   | 通过人数 |
| ---------------------------------- | ---- | ------------------------------------------------------------ | -------- |
| A. Payment Without Change          | √    |                                                              | 7365     |
| B. Minimize the Permutation        | √    | 看到$n \le 100$且$t \le 100$就该想直接想到暴力(优化成$O(n)$的意义不大) | 3716     |
| C. Platforms Jumping               | √    | 贪心 + 实现                                                  | 1320     |
| D. Binary String Minimizing        | √    | 贪心                                                         | 2583     |
| E. Yet Another Division Into Teams | √    | 一道带标记的Dp(Ps. 要是能注意到最优解中一个队伍不会超过5人，这题就更好做了(见题解)) | 392      |
| F. Equalizing Two Strings          | √    | 让B变成A，不如让AB都变成有序的串(详见代码)                   | 322      |

F题题解

当字符串s没有重复出现的字符时

> every swap of two adjacent elements changes the parity of the number of inversions



### Codeforces Round #605 (Div. 3)

[我的AC代码](https://gist.github.com/Chgtaxihe/987972772382a0a49f6c953e68cf2740)

| 题号                           | 完成 | 备注                     | 通过人数 |
| ------------------------------ | ---- | ------------------------ | -------- |
| A. Three Friends               | √    |                          | 6972     |
| B. Snow Walking Robot          | √    |                          | 4486     |
| C. Yet Another Broken Keyboard | √    |                          | 5061     |
| D. Remove One Element          | √    |                          | 2429     |
| E. Nearest Opposite Parity     | √    | 图论，痛哭涕流，看题解吧 | 594      |
| F. Two Bracket Sequences       | √    | 看了题解，是个三维Dp     | 188      |

F题题解

设`dp[i][j][k]`代表字符串`ans`的最小长度，其中`s[:i]`和`t[:j]`为`ans`的子序列，且`ans`中`(` - `)`的数量为`k`，可知如果`k`小于0，该字符串一定不合法，故有$0 \le k \le max(len(s), len(t))$

则可按如下规则更新`dp`

`dp[i+1][j][k+1] = dp[i][j][k] + 1 if s[i] == '('`

`dp[i][j+1][k+1] = dp[i][j][k] + 1 if t[j] == '('`

`dp[i+1][j+1][k+1] = dp[i][j][k] + 1 if s[i] == t[j] == '('`

`dp[i+1][j][k-1] = dp[i][j][k] + 1 if s[i] == ')'`

`dp[i][j+1][k-1] = dp[i][j][k] + 1 if t[j] == ')'`

`dp[i+1][j+1][k-1] = dp[i][j][k] + 1 if s[i] == t[j] == ')'`

同时根据定义，有

`dp[i][j][k] = min(self, dp[i][j][k+1] + 1, dp[i][j][k-1] + 1)`

则`dp[len(s)][len(t)][0]`为答案

按dp路径回溯即可得到`ans`                                                                                                     



### Codeforces Round #611 (Div. 3)

[题解](https://codeforces.com/contest/1283)

| 题号                           | 完成 | 备注 | 通过人数 |
| ------------------------------ | ---- | ---- | -------- |
| A. Minutes Before the New Year |      |      | 8731     |
| B. Candies Division            |      |      | 6998     |
| C. Friends and Gifts           |      |      | 2437     |
| D. Christmas Trees             |      |      | 1097     |
| E. New Year Parties            |      |      | 973      |
| F. DIY Garland                 |      |      | 177      |



### Codeforces Round #627 (Div. 3)

第一次AK，用了70分钟，就不记录了吧~

UPD: 打一场Rating就上1700+，我傻了



###  Codeforces Round #629 (Div. 3)

才过了4题，居然还能涨Rating...

| 题号                     | 完成         | 备注                                                         | 通过人数 |
| ------------------------ | ------------ | ------------------------------------------------------------ | -------- |
| A. Divisibility Problem  | 赛时-AC      |                                                              | 17088    |
| B. K-th Beautiful String | 赛时-AC      |                                                              | 9001     |
| C. Ternary XOR           | 赛时-AC      |                                                              | 9944     |
| D. Carousel              | 赛时-AC      |                                                              | 2266     |
| E. Tree Queries          | 赛时-TLE  AC |                                                              | 977      |
| F. Make k Equal          | 理论AC       | 要让(排序后的)左边出现$n$个$m$，首先让左边的数字全变为$m-1$，然后结果$+n$即可 | 368      |

E题题解

对于判断节点$u$是否在节点$v$到$root$的路径上

有一个巧妙的方法

```c++
void dfs(int v, int par = -1) {
    tin[v] = T++;
    for (auto to : g[v]) {
        if (to == par) continue;
        dfs(to, v);
    }
    tout[v] = T++;
}
```

对于$u$的子树上任意节点$v\ (v\ne u)$，有$tin[u]<tin[v]<tout[v]<tout[u]$





