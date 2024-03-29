---
layout: hidden_page
title: 斜率dp回顾
---

* auto-gen TOC:
{:toc}
# 斜率dp

对于类似$dp[i]=max(dp[j]+W_i+W_j+W_i'W_j'+C)$的转移方程（$W_i,W_i'$为与$i$有关的参数，$W_j,W_j'$为与$j$有关的参数，$C$为常数），可以通过单调性来优化



## 过程

对于$dp[k]$，设$F(x)=dp[x]+W_k+W_x+W_k'W_x'+C$，我们假设$dp[k]=max(F(i),F(j)),(i<j<k)$

假设$F(i)<F(j)$，那么有$dp[i]+W_i+W_k'W_i'<dp[j]+W_j+W_k'W_j'$

稍微化简一下，得

$(dp[j]+W_j)-(dp[i]+W_i)>W_k'(W_i'-W_j')$，假设$W_i'-W_j'<0$（大于零则不等号不需改变）

则有

$\frac{(dp[j]+W_j)-(dp[i]+W_i)}{W_i'-W_j'}<W_k'$

注意：若得到的$W_k'$**不具有单调性**，不可使用此方法！

令$G(x)=dp[x]+W_x,H(x)=-W_x$，则

$$\frac{G(j)-G(i)}{H(j)-H(i)}<W_k' \tag{1}$$

------

显然，$(1)$与斜率十分相似，该方法因此得名"斜率Dp"。

![](/resource/img/post/斜率dp_1.png)

如图所示，假设$dp[k]$可以转移自三个点$A,B,C$，且$k2<k1$。

考虑一下三种情况

1.  $W_k'<k2<k1$
2.  $k2<W_k'<k1$
3.  $k2<k1<W_k'$

对于情况1，根据$(1)$可知$A$点最优，同理，情况2时有$A$或$C$点最优，情况3时$C$点最优。无论如何$B$不可能为最优点，因而可以去除。

------

那么在继续引入任意个点后，有无可能使得$B$为最优点呢？

![](/resource/img/post/斜率dp_2.png)

如图所示，在引入新的点后，我们假设$B$点为最优点，那么说明此时$W_D'>k1$

又因为$k1>k2$，所以$W_D'>k2$，因此$C$点优于$B$点，与假设不符。

------

通过上述做法，我们能够得到一个下凸包（斜率单调递增，一般使用队列来维护）。对于给定的$W_k'$，只需要寻找线段$AB$，使得该线段为队列中第一段满足斜率$sloop_{AB}\ge W_k$的线段，一般可以使用二分法来解决。

特别的，对于$(1)$，若$W_k'$**单调递增**，又因为维护的队列中斜率也是**单调递增**的，则可以通过把队头中$sloop<W_k'$的线段全部弹出，之后队头元素即为最优点。

------

总结一下，维护的凸包是上凸还是下凸，取决于不等号：

1.  若$(1)$是形如$sloop<W_k$的式子，则维护下凸包
2.  若$(1)$是形如$sloop>W_k$的式子，则维护上凸包



# 例题 Gym 102202E

首先，设长方形$i$的面积为$A_i$，宽为$W_i$，高为$H_i$，约定$W_i\ge H_i$，所有长方形的面积之和为$S_A=\sum A_i$，所有长方形的宽之和为$S_W=\sum W_i$。

若选定两个长方形$(i,j)(i\ne j,W_i\ge W_j)$作为两侧的边界，设得到的容积为$V_{ij}$，则有

$$V_{ij}\ge W_j*(S_w-W_i-W_j)-(S_A+A_i+A_j)$$

之所以是**大于等于**而非**等于**，是因为容器内可能存在比两侧长方形更高的长方形（即存在$x\not\in\{i,j\}, H_x>W_j$），但此类方案不可能为最优解，因而不影响最终结果。

得到上述面积公式后，可以把长方形按$W_i$降序排列（升序也行，只不过公式稍微复杂一些）

按照斜率Dp的做法，可以得到如下式子

$\frac{A_i-A_j}{W_i-W_j}<W_k\ (i<j<k) \text{若k从j转移优于从i转移}$

转移时，二分查找最优转移点即可。

------

AC代码如下:

```c++
#include <bits/stdc++.h>
#define ll long long
#define Android ios::sync_with_stdio(false), cin.tie(NULL)

using namespace std;
using pll = pair<ll, ll>;

const int maxn = 3e5 + 1000;

ll n, sum_area = 0, sum_width = 0;
pll box[maxn];
int que[maxn], tail = 0;

ll bin_search(ll l, ll r, std::function<bool(ll)> check){
    ll result = l, mid;
    while(l <= r){
        mid = (l + r) >> 1;
        if(check(mid)){
            result = mid;
            r = mid - 1;
        }else{
            l = mid + 1;
        }
    }
    return result;
}

inline ll area(int p){return box[p].first * box[p].second;}

ll get_ans(int i, int j){
    if(box[i].first < box[j].first) swap(i, j);
    return box[j].first * (sum_width - box[i].first - box[j].first) - sum_area + area(i) + area(j);
}

ll k;
bool check(ll mid){
    return (box[que[mid]].first - box[que[mid + 1]].first) * k >= area(que[mid]) - area(que[mid + 1]);
}

void solve(){
    cin >> n;
    for(int i=1; i<=n; i++) {
        cin >> box[i].first >> box[i].second;
        if(box[i].first < box[i].second) swap(box[i].first, box[i].second);
        sum_area += area(i);
        sum_width += box[i].first;
    }
    sort(box + 1, box + 1 + n, [](pll a, pll b){
        if(a.first != b.first) return a.first > b.first;
        return a.second > b.second; // 第二关键字随意
    });
    ll ans = 0;
    for(int i=1; i<=n; i++){
        k = box[i].first; // 即W_k'
        if(tail > 0){
            ll pos = 0;
            if(tail > 1){
                pos = bin_search(0, tail - 2, check);
                if(check(pos)) pos++;
            }
            ans = max(ans, get_ans(que[pos], i));
        }
        while(tail > 1 && (area(que[tail-1]) - area(i)) * (box[que[tail-2]].first - box[que[tail-1]].first) 
            <= (area(que[tail-2]) - area(que[tail-1])) * (box[que[tail-1]].first - box[i].first)) tail--;
        que[tail++] = i;
    }
    cout << ans << '\n';
}

signed main(){
    Android;
    solve();
}

```



