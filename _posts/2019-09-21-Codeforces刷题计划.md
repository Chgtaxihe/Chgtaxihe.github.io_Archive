---
layout: post
title: Codeforces 刷题计划
tags: algorithm Codeforces
---

# Codeforces Rua~

* auto-gen TOC:
{:toc}
## 说明

有些题目比较简单，就没写题解/AC代码啦

## Div. 1

### [Codeforces Round #609 (Div. 1)](https://codeforces.com/contest/1268)

[题解](https://codeforces.com/blog/entry/72358)

[我的AC代码]

| 题号                                                         | 完成 | 备注        | 过题人数 |
| ------------------------------------------------------------ | ---- | ----------- | -------- |
| D. [Invertation in Tournament](https://codeforces.com/contest/1268/problem/D) |      | 我不配 ╥﹏╥ | 93       |
| E. [Happy Cactus](https://codeforces.com/contest/1268/problem/E) |      |             | 58       |



## Div. 2

### [Codeforces Round #588 (Div. 2)](https://codeforces.com/contest/1230) 

[题解](https://codeforces.com/blog/entry/70008) [VirtualJudge](https://vjudge.net/problem#OJId=CodeForces&probNum=1230)

[我的AC代码(C/D/E/F)](https://gist.github.com/Chgtaxihe/3f79063816b1224702acc31e684011aa)

| 题号                                                         | 完成 | 一句话题解                                                   |
| ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| A. [Dawid and Bags of Candies](https://codeforces.com/contest/1230/problem/A) | √    |                                                              |
| B. [Ania and Minimizing](https://codeforces.com/contest/1230/problem/B) | √    |                                                              |
| C. [Anadi and Domino](https://codeforces.com/contest/1230/problem/C) | √    | 如果n = 7，那么一定有两个点公用一个数字                      |
| D. [Marcin and Training Camp](https://codeforces.com/contest/1230/problem/D) | √    | 如果A和B不是子集关系，那么A比B强且B比A强，$O(n^2)$           |
| E. [Kamil and Making a Stream](https://codeforces.com/contest/1230/problem/E) | √    | AC容易，证明复杂度不易($v$到$v$的祖先路径上的不同的$gcd$不会超过$log(10^12)$个) |
| F. [Konrad and Company Evaluation](https://codeforces.com/contest/1230/problem/F) | √    | $ans = \sum OutDegree_i * InDegree_i$ </br>难点在于证明复杂度$O(n + m + q \sqrt{2m})$ |



### [Educational Codeforces Round 73](https://codeforces.com/contest/1221) 

(Virtual Participate)

| 题号                                                         | 完成 | 一句话题解                                                   | 过题人数 |
| ------------------------------------------------------------ | ---- | ------------------------------------------------------------ | -------- |
| A. [2048 Game](https://codeforces.com/contest/1221/problem/A) | √    |                                                              | 5662     |
| B. [Knights](https://codeforces.com/contest/1221/problem/B)  | √    | 随便猜个结论，居然过了？？？                                 | 4135     |
| C. [Perfect Team](https://codeforces.com/contest/1221/problem/C) | √    |                                                              | 4776     |
| D. [Make The Fence Great Again](https://codeforces.com/contest/1221/problem/D) | √    | 每个板子增加的长度不会超过2，故$$dp_{pos, add} = add \cdot b_{pos} + \min\limits_{x=0 \dots 2, a_{pos-1}+x \neq a_{pos}+add} dp_{pos-1, x}$$ | 1426     |
| E. [Game With String](https://codeforces.com/contest/1221/problem/E) | √    | 不容易啊，[题解](https://codeforces.com/blog/entry/69925)    | 122      |
| F. [Choose a Square](https://codeforces.com/contest/1221/problem/F) | ╳    |                                                              | 85       |
| G. [Graph And Numbers](https://codeforces.com/contest/1221/problem/G) | ╳    |                                                              | 12       |



### [Codeforces Round #589 (Div. 2)](https://codeforces.com/contest/1228)

[题解](https://codeforces.com/blog/entry/70162) [VirtualJudge](https://vjudge.net/problem#OJId=CodeForces&probNum=1228)

[我的AC代码(C/D/E)](https://gist.github.com/Chgtaxihe/0775c7faff399a4fcce0bcac8b203574)

| 题号                                                         | 完成 | 一句话题解                  | 过题人数 |
| ------------------------------------------------------------ | ---- | --------------------------- | -------- |
| A. [Distinct Digits](https://codeforces.com/contest/1228/problem/A) | √    |                             | 10912    |
| B. [Filling the Grid](https://codeforces.com/contest/1228/problem/B) | √    | 暴力模拟                    | 6921     |
| C. [Primes and Multiplication](https://codeforces.com/contest/1228/problem/C) | √    | 数学太恐怖，去看题解吧      | 4559     |
| D. [Complete Tripartite](https://codeforces.com/contest/1228/problem/D) | √    | 优雅的暴力                  | 2842     |
| E. [Another Filling the Grid](https://codeforces.com/contest/1228/problem/E) | √    | [DP] 题解表述有误，看评论区 | 965      |
| F. [One Node is Gone](https://codeforces.com/contest/1228/problem/F) |      |                             | 209      |



### [Educational Codeforces Round 74](https://codeforces.com/contest/1238)
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



### [Codeforces Round #592 (Div. 2) ](https://codeforces.com/contest/1244)

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



### [Codeforces Round #593 (Div. 2)](https://codeforces.com/contest/1236)

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



### [Codeforces Round #594 (Div. 2) ]( https://codeforces.com/contest/1248 )

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



### [Educational Codeforces Round 75 (Rated for Div. 2)](https://codeforces.com/contest/1251)

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



### [Codeforces Round #597 (Div. 2)](https://codeforces.com/contest/1245)

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



###  [Codeforces Round #599 (Div. 2) ](https://codeforces.com/contest/1243)

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

#### C题题解

对于$n=p^k$(p为质数)，有$ans = p$ (A)

对于$n = pq$ ($gcd(p, q) = 1$)，有$ans=1$ (B)

下面对(B)进行证明

对于任意$i$和$j(i\neq j)$，存在$1 \le x \le n$使得$x \equiv i \pmod{p}$且$x \equiv j \pmod{q}$(中国剩余定理)

因此$i$和$j(i\neq j)$颜色与$x$相同

#### D题题解

暴力即可(set/bitset记录连通块)



### [Educational Codeforces Round 76 (Rated for Div. 2)](https://codeforces.com/contest/1257)

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



### [Codeforces Round #600 (Div. 2)](https://codeforces.com/contest/1253)

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



### [Codeforces Round #601 (Div. 2)](https://codeforces.com/contest/1255)

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



###  [Educational Codeforces Round 77 (Rated for Div. 2)](https://codeforces.com/contest/1260)

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

#### C题题解

假定$r\le b$， $g=gcd(r, b)$，存在$rx - by = g$ ($y\ge0$)，即$rx = g + by$ ($y\ge0$)

则对于两个相邻的蓝色块$by$与$by + b$，我们要在其中插入$m+1$个红色块，

$by+g, by+g+r, by+g+2r,...,by+g+(m*r)$

且 $by+g+(m*r) < by+b$

也就是说$m+1 \ge k$，即$g + (k-1)*r < b$ 时`REBEL`，否则`OBEY`



### [Codeforces Round #603 (Div. 2)](https://codeforces.com/contest/1263)

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

#### F题题解

以`cursor`为界，分为左右两部分。同时计算左侧前缀和、右侧后缀和("("计1，")"计-1)。

若左侧合法，则定有$min(sum_{left}) \ge 0$，右侧合法则定有$max(sum_{right}) \le 0$

若整个串合法，除上述条件外，$sum_{left} + sum_{right}=0$

那么最大深度为$max(sum_{left}, max(sum_{left}), -min(sum_{right}))$

复杂度$O( n )$



### [Codeforces Round #604 (Div. 2)](https://codeforces.com/contest/1265)

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

#### E题题解

没什么好说的，概率dp

$cost_i = cost_{i-1} + 1 + (1-p_i)cost_i$

#### F题待完成！！！



### [Codeforces Round #607 (Div. 2)](https://codeforces.com/contest/1281)

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



### [Codeforces Round #608 (Div. 2)](https://codeforces.com/contest/1271)

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



### [Educational Codeforces Round 78 (Rated for Div. 2)](https://codeforces.com/contest/1278)

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



### [Codeforces Round #609 (Div. 2)](https://codeforces.com/contest/1269)

[题解](https://codeforces.com/blog/entry/72358)

[我的AC代码](https://gist.github.com/Chgtaxihe/ca4af5c0f847fab5f4589e00648b395d)

| 题号                                                         | 完成 | 备注                                                         | 通过人数 |
| ------------------------------------------------------------ | ---- | ------------------------------------------------------------ | -------- |
| A. [Equation](https://codeforces.com/contest/1269/problem/A) | √    |                                                              | 9859     |
| B. [Modulo Equality](https://codeforces.com/contest/1269/problem/B) | √    | 这题用dict/map做，代码量会少一点                             | 5103     |
| C. [Long Beautiful Integer](https://codeforces.com/contest/1269/problem/C) | √    | 脑子没转过来，漏判一个条件~怎么回事??????                    | 3471     |
| D. [Domino for Young](https://codeforces.com/contest/1269/problem/D) | √    | [**思维**]如果把图按棋盘的方式涂色，那么一个`domino`永远会占用一黑一白两种颜色的格子 | 1945     |
| E. [K Integers](https://codeforces.com/contest/1269/problem/E) | √    | 看不懂题解。。估计是我境界不够                               | 253      |

#### E题题解

题解讲的不是很清楚，这里做一下记录

首先，对于一个定值$k$，我们来讨论一下如何求解:

首先计算原序列中`1 - k`中的逆序对数为$inv$， 接下来我们改变一下原序列

`arr = [1 if x <= k else 0 for x in arr]`

这样任务就变成了计算产生$k$个连续的1所需的操作步数，显然只需要把所有数字移动到中位即可



那么对于$1 \le k \le n$，只需用一个树状数组维护逆序对和中位，并将$k$从1遍历到$n$即可求出答案。

（统计答案时可以用树状数组计算前缀和，因此代码中一共了两个树状数组）



### [Codeforces Round #610 (Div. 2)](https://codeforces.com/contest/1282)

[题解](https://codeforces.com/blog/entry/72461)

[我的AC代码](https://gist.github.com/Chgtaxihe/b89358bd1628631bdcd5a9a33537a24a)

| 题号                                                         | 完成 | 备注                                     | 通过人数 |
| ------------------------------------------------------------ | ---- | ---------------------------------------- | -------- |
| A. [Temporarily unavailable](https://codeforces.com/contest/1282/problem/A) | √    |                                          | 9204     |
| B1. [K for the Price of One (Easy Version)](https://codeforces.com/contest/1282/problem/B1) | √    | [贪心]                                   | 6128     |
| B2. [K for the Price of One (Hard Version)](https://codeforces.com/contest/1282/problem/B2) | √    | [贪心]                                   | 5059     |
| C. [Petya and Exam](https://codeforces.com/contest/1282/problem/C) | √    | [**贪心**]在$t_i - 1$时刻离开是最佳的    | 2532     |
| D. [Enchanted Artifact](https://codeforces.com/contest/1282/problem/D) | √    | [**思维**]关键在于如何求出`a`和`b`的数量 | 1255     |
| E. [The Cake Is a Lie](https://codeforces.com/contest/1282/problem/E) |      |                                          | 595      |



### [Educational Codeforces Round 79 (Rated for Div. 2)](https://codeforces.com/contest/1279)

[题解](https://codeforces.com/blog/entry/72577)

[我的AC代码](https://gist.github.com/Chgtaxihe/d86643d5f6fb1634e359df0df973057e)

| 题号                                                         | 完成 | 备注                                                         | 通过人数 |
| ------------------------------------------------------------ | ---- | ------------------------------------------------------------ | -------- |
| A. [New Year Garland](https://codeforces.com/contest/1279/problem/A) | √    |                                                              | 6821     |
| B. [Verse For Santa](https://codeforces.com/contest/1279/problem/B) | √    | **如果只能背到第x段，那么跳过大于x的段落是没用的！**不然就WA | 4492     |
| C. [Stack of Presents](https://codeforces.com/contest/1279/problem/C) | √    |                                                              | 3687     |
| D. [Santa's Bot](https://codeforces.com/contest/1279/problem/D) | √    | 除了A之外最简单的一题？                                      | 1672     |
| E. [New Year Permutations](https://codeforces.com/contest/1279/problem/E) |      | 感觉可以做，但是过题人数有点恐怖                             | 32       |
| F. [New Year and Handle Change](https://codeforces.com/contest/1279/problem/F) |      |                                                              | 36       |




## Div. 3

### [Codeforces Round #587 (Div. 3)](https://codeforces.com/contest/1216)

[题解](https://codeforces.com/blog/entry/69954) [VirtualJudge](https://vjudge.net/problem#OJId=CodeForces&probNum=1216&title=&source=&category=all)

[我的AC代码(C/E2/F)](https://gist.github.com/Chgtaxihe/7a268e89d6d5913ef37a8948d7f7c6b2)

| 题号                                                         | 完成 | 一句话题解 | 通过人数 |
| ------------------------------------------------------------ | ---- | ---------- | -------- |
| A. [Prefixes](https://codeforces.com/contest/1216/problem/A) | √    | Water      | 5931     |
| B. [Shooting](https://codeforces.com/contest/1216/problem/B) | √    |            | 5577     |
| C. [White Sheet](https://codeforces.com/contest/1216/problem/C) | √    | 有点小麻烦 | 1331     |
| D. [Swords](https://codeforces.com/contest/1216/problem/D)   | √    |            | 3388     |
| E1. [Numerical Sequence (easy version)](https://codeforces.com/contest/1216/problem/E1) | √    |            | 670      |
| E2. [Numerical Sequence (hard version)](https://codeforces.com/contest/1216/problem/E2) | √    | 不容易啊   | 128      |
| F. [Wi-Fi](https://codeforces.com/contest/1216/problem/F)    | √    | DP好难     | 185      |



### [Codeforces Round #590 (Div. 3)](https://codeforces.com/contest/1234)

[题解](https://codeforces.com/blog/entry/70233) [VirtualJudge](https://vjudge.net/problem#OJId=CodeForces&probNum=1234&title=&source=&category=all)

[我的AC代码(B2/D/E/F)](https://gist.github.com/Chgtaxihe/77b664c4c8a4295140c6310a23b218e2)

| 题号                                                         | 完成 | 一句话题解                                                   | 通过人数 |
| ------------------------------------------------------------ | ---- | ------------------------------------------------------------ | -------- |
| A. [Equalize Prices Again](https://codeforces.com/contest/1234/problem/A) | √    |                                                              | 8366     |
| B1. [Social Network (easy version)](https://codeforces.com/contest/1234/problem/B1) | √    |                                                              | 6851     |
| B2. [Social Network (hard version)](https://codeforces.com/contest/1234/problem/B2) | √    | 我服了，出题人专门出了一组数据来Hack unordered_set，用set即或[自定义hash](https://codeforces.com/blog/entry/62393) | 4712     |
| C. [Pipes](https://codeforces.com/contest/1234/problem/C)    | √    |                                                              | 2924     |
| D. [Distinct Characters Queries](https://codeforces.com/contest/1234/problem/D) | √    | 看题解半天都看不懂，才发现是读错题了                         | 2035     |
| E. [Special Permutations](https://codeforces.com/contest/1234/problem/E) | √    |                                                              | 455      |
| F. [Yet Another Substring Reverse](https://codeforces.com/contest/1234/problem/F) | √    | 感觉这题比F简单，刚开始还以为是水过的（毕竟DFS），后来发现只要把DFS改成一个for就是正解了 | 151      |



### [Codeforces Round #595 (Div. 3)](https://codeforces.com/contest/1249)

[题解](https://codeforces.com/blog/entry/70779)

[我的AC代码(F题)](https://gist.github.com/Chgtaxihe/83ff3d95037537d11a3d9cbe51020b11)

| 题号                                                         | 完成 | 一句话题解                                                   | 通过人数 |
| ------------------------------------------------------------ | ---- | ------------------------------------------------------------ | -------- |
| A. [Yet Another Dividing into Teams](https://codeforces.com/contest/1249/problem/A) | √    |                                                              | 8354     |
| B1. [Books Exchange (easy version)](https://codeforces.com/contest/1249/problem/B1) | √    |                                                              | 7001     |
| B2. [Books Exchange (hard version)](https://codeforces.com/contest/1249/problem/B2) | √    |                                                              | 4520     |
| C1. [Good Numbers (easy version)](https://codeforces.com/contest/1249/problem/C1) | √    |                                                              | 4500     |
| C2. [Good Numbers (hard version)](https://codeforces.com/contest/1249/problem/C2) | √    |                                                              | 2785     |
| D1. [Too Many Segments (easy version)](https://codeforces.com/contest/1249/problem/D1) | √    |                                                              | 893      |
| D2. [Too Many Segments (hard version)](https://codeforces.com/contest/1249/problem/D2) | √    |                                                              | 726      |
| E. [By Elevator or Stairs?](https://codeforces.com/contest/1249/problem/E) | √    |                                                              | 1483     |
| F. [Maximum Weight Subset](https://codeforces.com/contest/1249/problem/F) | √    | [**树Dp**] `dp[u][dep]`代表以`u`为根的子树中，被选取的点深度至少为`dep`时最大的`weight`之和 | 152      |



### [Codeforces Round #598 (Div. 3)](https://codeforces.com/contest/1256)

[题解](https://codeforces.com/blog/entry/71184)

[我的AC代码（C/D/E/F）](https://gist.github.com/Chgtaxihe/609ee28d9f9e40b2dc7cad4f54c08ec7)

| 题号                                                         | 完成 | 一句话题解                                                   | 通过人数 |
| ------------------------------------------------------------ | ---- | ------------------------------------------------------------ | -------- |
| A. [Payment Without Change](https://codeforces.com/contest/1256/problem/A) | √    |                                                              | 7365     |
| B. [Minimize the Permutation](https://codeforces.com/contest/1256/problem/B) | √    | 看到$n \le 100$且$t \le 100$就该想直接想到暴力(优化成$O(n)$的意义不大) | 3716     |
| C. [Platforms Jumping](https://codeforces.com/contest/1256/problem/C) | √    | 贪心 + 实现                                                  | 1320     |
| D. [Binary String Minimizing](https://codeforces.com/contest/1256/problem/D) | √    | 贪心                                                         | 2583     |
| E. [Yet Another Division Into Teams](https://codeforces.com/contest/1256/problem/E) | √    | 一道带标记的Dp(Ps. 要是能注意到最优解中一个队伍不会超过5人，这题就更好做了(见题解)) | 392      |
| F. [Equalizing Two Strings](https://codeforces.com/contest/1256/problem/F) | √    | 让B变成A，不如让AB都变成有序的串(详见代码)                   | 322      |

#### F题题解

当字符串s没有重复出现的字符时

> every swap of two adjacent elements changes the parity of the number of inversions



### [Codeforces Round #605 (Div. 3)](https://codeforces.com/contest/1272)

[题解](https://codeforces.com/blog/entry/72132)

[我的AC代码](https://gist.github.com/Chgtaxihe/987972772382a0a49f6c953e68cf2740)

| 题号                                                         | 完成 | 备注                     | 通过人数 |
| ------------------------------------------------------------ | ---- | ------------------------ | -------- |
| A. [Three Friends](https://codeforces.com/contest/1272/problem/A) | √    |                          | 6972     |
| B. [Snow Walking Robot](https://codeforces.com/contest/1272/problem/B) | √    |                          | 4486     |
| C. [Yet Another Broken Keyboard](https://codeforces.com/contest/1272/problem/C) | √    |                          | 5061     |
| D. [Remove One Element](https://codeforces.com/contest/1272/problem/D) | √    |                          | 2429     |
| E. [Nearest Opposite Parity](https://codeforces.com/contest/1272/problem/E) | √    | 图论，痛哭涕流，看题解吧 | 594      |
| F. [Two Bracket Sequences](https://codeforces.com/contest/1272/problem/F) | √    | 看了题解，是个三维Dp     | 188      |

#### F题题解

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



### [Codeforces Round #611 (Div. 3)](https://codeforces.com/contest/1283)

[题解](https://codeforces.com/contest/1283)

[我的AC代码]

| 题号                                                         | 完成 | 备注 | 通过人数 |
| ------------------------------------------------------------ | ---- | ---- | -------- |
| A. [Minutes Before the New Year](https://codeforces.com/contest/1283/problem/A) |      |      | 8731     |
| B. [Candies Division](https://codeforces.com/contest/1283/problem/B) |      |      | 6998     |
| C. [Friends and Gifts](https://codeforces.com/contest/1283/problem/C) |      |      | 2437     |
| D. [Christmas Trees](https://codeforces.com/contest/1283/problem/D) |      |      | 1097     |
| E. [New Year Parties](https://codeforces.com/contest/1283/problem/E) |      |      | 973      |
| F. [DIY Garland](https://codeforces.com/contest/1283/problem/F) |      |      | 177      |

