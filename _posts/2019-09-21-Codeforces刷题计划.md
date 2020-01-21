---
layout: post
title: Codeforces 刷题计划
tags: algorithm Codeforces
---

# Codeforces Rua~

* auto-gen TOC:
{:toc}
## 说明

1. 有些题目比较简单，就没写题解/AC代码啦

## Div. 1

还没到那个级别呢～



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
| A. [2048 Game](https://codeforces.com/contest/1221/problem/A) | AC   |                                                              | 5662     |
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
| F. [One Node is Gone](https://codeforces.com/contest/1228/problem/F) | ╳    |                             | 209      |



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

| 题号                                                         | 完成 | 备注 | 通过人数 |
| ------------------------------------------------------------ | ---- | ---- | -------- |
| A. [Changing Volume](https://codeforces.com/contest/1255/problem/A) |      |      |          |
| B. [Fridge Lockers](https://codeforces.com/contest/1255/problem/B) |      |      |          |
| C. [League of Leesins](https://codeforces.com/contest/1255/problem/C) |      |      |          |
| D. [Feeding Chicken](https://codeforces.com/contest/1255/problem/D) |      |      |          |
| E1. [Send Boxes to Alice (Easy Version)](https://codeforces.com/contest/1255/problem/E1) |      |      |          |
| E2. [Send Boxes to Alice (Hard Version)](https://codeforces.com/contest/1255/problem/E2) |      |      |          |
| F. [Point Ordering](https://codeforces.com/contest/1255/problem/F) |      |      |          |




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