---
layout: hidden_page
title: IDA*学习笔记
---

* auto-gen TOC:
{:toc}


# IDA*学习笔记

我们知道A\*是针对BFS的优化，那么DFS能不能也套用A\*的思想进行优化呢？显然可以



## 迭代加深

dfs中经常遇到这样的问题：正确答案所在的分支深度只有$x$，但是搜索时到达了深度$y>>x$。

迭代加深可以缓解这种情况

```c++
bool dfs(info data, int step, int limit){
	if(step > limit) return false;
    // do something
}
......
for(int i=1; i<max; i++){
    if(dfs(data, 0, i)) return true;
}
```

上面便是一个迭代加深的算法



## IDA*

稍微修改一下便可以得到

```c++
bool dfs(info data, int step, int limit){
	if(estimate() + step > limit) return false;
    // do something
}
......
for(int i=1; i<max; i++){
    if(dfs(data, 0, i)) return true;
}
```

其中`estimate()`是估值函数，用于估计离结束还有多少步

这里的`estimate()`不一定是实际值，但一定要**小于等于实际值**，否则不能保证得到最优解

 

## 例题 洛谷P2324

```c++
#include <bits/stdc++.h>
#define ll long long

char grid[5][6];
char target[5][6] = {
    "11111",
    "01111",
    "00*11",
    "00001",
    "00000"
};
int delta_x[] = {-2, -2, -1, -1, 1, 1, 2, 2};
int delta_y[] = {1, -1, 2, -2, 2, -2, 1, -1};

int diff(){
    int cnt = 0;
    for(int i=0; i<5; i++)
        for(int j=0; j<5; j++)
            cnt += grid[i][j] != target[i][j];
    if(cnt > 0) cnt--;
    return cnt;
}

bool dfs(int x, int y, int limit, int cur, int prev){
    int estimate = diff();
    if(estimate + cur > limit) return false; // 剪枝1
    if(estimate == 0) return true; // 成功
    for(int i=0; i<8; i++){
        if(7 - i == prev) continue; // 剪枝2:如果当前步与前一步刚好抵消，则不可能是最优
        int nx = x + delta_x[i];
        int ny = y + delta_y[i];
        if(nx >= 5 || nx < 0 || ny >= 5 || ny < 0) continue;
        swap(grid[x][y], grid[nx][ny]);
        if(dfs(nx, ny, limit, cur+1, i)) return true;
        swap(grid[x][y], grid[nx][ny]);
    }
    return false;
}

void solve(){
    for(int i=0; i<5; i++) cin >> grid[i];
    int x=0, y=0;
    for(int i=0; i<5; i++){
        for(int j=0; j<5; j++) {
            if(grid[i][j] == '*') x = i, y = j;
        }
    }
    for(int i=1; i<=15; i++){
        if(dfs(x, y, i, 0, 8)) {
            cout << i << "\n";
            return;
        }
    }
    cout << "-1\n";
}

signed main(){
    int t;
    cin >> t;
    while(t--)
    solve();
}
```



## 例题 HDU 1043

这道题的关键在于：把拼图按行压成一维序列，忽略`x`，可以发现每次操作后，序列的逆序对的奇偶性不变！

耗时：迭代加深+15(78ms)，迭代加深+10(78ms)，迭代加深+1(171ms)

```c++
#include <bits/stdc++.h>

using namespace std;

char grid[3][3];
int delta_x[] = {-1, 0, 0, 1};
int delta_y[] = {0, 1, -1, 0};
char cor[] = "urld";

int diff(){
    int cnt = 0, x;
    for(int i=0; i<3; i++)
        for(int j=0; j<3; j++){
            x = grid[i][j] - '0';
            if(x) cnt += abs(i-(x-1)/3) + abs(j-(x-1)%3);
        }
    return cnt;
}

char ans[300], * ans_ptr;
bool dfs(int x, int y, int step, int limit, int prev){
    int estimate = diff();
    if(estimate + step > limit) return false;
    if(estimate == 0) return true;
    for(int i=0; i<4; i++){
        if(3-prev == i) continue;
        int nx = x + delta_x[i];
        int ny = y + delta_y[i];
        if(nx < 0 || nx >= 3 || ny < 0 || ny >= 3) continue;
        swap(grid[nx][ny], grid[x][y]);
        if(dfs(nx, ny, step+1, limit, i)){
            *(ans_ptr++) = cor[i];
            return true;
        }
        swap(grid[nx][ny], grid[x][y]);
    }
    return false;
}

void solve(){
    int inverse = 0;
    int k[10];
    for(int i=0; i<3; i++)
        for(int j=0; j<3; j++) {
            if(grid[i][j] == 'x') grid[i][j] = '0';
            k[i*3+j]=grid[i][j] - '0';
        }
    for(int i=0; i<9; i++){
        if(k[i] == 0) continue;
        for(int j=0; j<i; j++) inverse += (k[j] != 0 && k[j] > k[i]);
    }
    if(inverse & 1){ // 特判，否则TLE
        cout << "unsolvable\n";
        return;
    }

    int x, y;
    for(int i=0; i<3; i++){
        for(int j=0; j<3; j++) if(grid[i][j] == '0') {
            x = i, y = j;
        }
    }
    ans_ptr = ans;
    for(int i=1; i<=76; i+=10) // +10，耗时比+1更短
        if(dfs(x, y, 0, i, -1)) break;
    ans_ptr--;
    while((ans_ptr+1) != ans) cout << *(ans_ptr--);
    cout << endl;
}

signed main(){
    char c = getchar();
    while(c != EOF){
        while(c == '\n' || c == ' ') c = getchar();
        if(c == EOF) break;
        for(int i=0; i<9; i++){
            while(c == ' ') c = getchar();
            grid[i/3][i%3] = c;
            c = getchar();
        }
        solve();
    }
}
```

