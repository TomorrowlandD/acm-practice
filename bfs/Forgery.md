# Forgery

https://codeforces.com/problemset/problem/1059/B

## 题面翻译

给定一个$n,m$的目标矩阵。

**初始矩阵全为$'.'$**

你可以染色无数次，每次选定一个格子将它周围的八个格子（除它自己）的3*3矩阵覆盖成'#'。

这个3*3的矩阵只能出现在$n*m$的矩阵内部。不能越界。

询问是否能构成目标矩阵。

## 题目描述

Student Andrey has been skipping physical education lessons for the whole term, and now he must somehow get a passing grade on this subject. Obviously, it is impossible to do this by legal means, but Andrey doesn't give up. Having obtained an empty certificate from a local hospital, he is going to use his knowledge of local doctor's handwriting to make a counterfeit certificate of illness. However, after writing most of the certificate, Andrey suddenly discovered that doctor's signature is impossible to forge. Or is it?

For simplicity, the signature is represented as an $ n\times m $ grid, where every cell is either filled with ink or empty. Andrey's pen can fill a $ 3\times3 $ square without its central cell if it is completely contained inside the grid, as shown below.

 `<br></br>xxx<br></br>x.x<br></br>xxx<br></br>`Determine whether is it possible to forge the signature on an empty $ n\times m $ grid.

## 输入格式

The first line of input contains two integers $ n $ and $ m $ ( $ 3 \le n, m \le 1000 $ ).

Then $ n $ lines follow, each contains $ m $ characters. Each of the characters is either '.', representing an empty cell, or '\#', representing an ink filled cell.

## 输出格式

If Andrey can forge the signature, output "YES". Otherwise output "NO".

You can print each letter in any case (upper or lower).

## 样例 #1

### 样例输入 #1

```
3 3
###
#.#
###
```

### 样例输出 #1

```
YES
```

## 样例 #2

### 样例输入 #2

```
3 3
###
###
###
```

### 样例输出 #2

```
NO
```

## 样例 #3

### 样例输入 #3

```
4 3
###
###
###
###
```

### 样例输出 #3

```
YES
```

## 样例 #4

### 样例输入 #4

```
5 7
.......
.#####.
.#.#.#.
.#####.
.......
```

### 样例输出 #4

```
YES
```

## 提示

In the first sample Andrey can paint the border of the square with the center in $ (2, 2) $ .

In the second sample the signature is impossible to forge.

In the third sample Andrey can paint the borders of the squares with the centers in $ (2, 2) $ and $ (3, 2) $ :

1. we have a clear paper: `<br></br>...<br></br>...<br></br>...<br></br>...<br></br>`
2. use the pen with center at $ (2, 2) $ . `<br></br>###<br></br>#.#<br></br>###<br></br>...<br></br>`
3. use the pen with center at $ (3, 2) $ . `<br></br>###<br></br>###<br></br>###<br></br>###<br></br>`

In the fourth sample Andrey can paint the borders of the squares with the centers in $ (3, 3) $ and $ (3, 5) $ .

## 思路：

这题我感觉更像模拟题，不像bfs的题目。这题我们只需要枚举所有的点，发现这个点可以进行染色，那么我们就染这个点，否则就不染。最后判断染色完的地图和我们的目标地图是否完全相等即可。

## 代码:

```c++
#include<bits/stdc++.h>
using namespace std;
char mp[1005][1005];
char goal[1005][1005];
int n,m;
int dx[]{-1, -1, 0, 1, 1, 1, 0, -1};
int dy[]{0, 1, 1, 1, 0, -1, -1, -1};
bool check()
{
    for(int i=1;i<=n;i++){
        for(int j=1;j<=m;j++){
            if(mp[i][j]!=goal[i][j]) return false;
        }
    }
    return true;
}
int main()
{
    cin>>n>>m;
    for(int i=1;i<=n;i++){
        for(int j=1;j<=m;j++){
            cin>>goal[i][j];
            mp[i][j]='.';
        }
    }
    //枚举每一个点，判断这个点能不能进行染色，若可以进行染色，就染它周围的八个点 
    for(int i=1;i<=n;i++){
        for(int j=1;j<=m;j++){
            int f=1;
            for(int t=0;t<8;t++){
                int a=i+dx[t];
                int b=j+dy[t];
                //旁边有越界的点，就不染
                if(a<1||b<1||a>n||b>m) {f=0;break;}
                //旁边8个点有不是'#'的点，就不染。
                if(goal[a][b]!='#') {f=0;break;}
            }
            //若点不能进行染色，就不染这个点。
            if(!f) continue;
            //否则，将旁边8个点全部染成'#'
            for(int t=0;t<8;t++){
                mp[i+dx[t]][j+dy[t]]='#';
            }
        }
    }
    
    if(!check()) cout<<"NO\n";
    else cout<<"YES\n";
    return 0;
}
```

