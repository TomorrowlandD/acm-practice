# [BalticOI 2011 Day1] Switch the Lamp On 电路维修

https://www.luogu.com.cn/problem/P4667

## 题面翻译

### 题目描述
Casper 正在设计电路。有一种正方形的电路元件，在它的两组相对顶点中，有一组会用导线连接起来，另一组则不会。有 $N\times M$ 个这样的元件，你想将其排列成 $N$ 行，每行 $M$ 个。 电源连接到板的左上角。灯连接到板的右下角。只有在电源和灯之间有一条电线连接的情况下，灯才会亮着。为了打开灯，任何数量的电路元件都可以转动 90°（两个方向）。

![](https://cdn.luogu.com.cn/upload/pic/1286.png)

![](https://cdn.luogu.com.cn/upload/pic/1285.png)

在上面的图片中，灯是关着的。如果右边的第二列的任何一个电路元件被旋转 90°，电源和灯都会连接，灯被打开。现在请你编写一个程序，求出最小需要多少旋转多少电路元件。

### 输入输出格式

#### 输入格式
输入的第一行包含两个整数 $N$ 和 $M$，表示盘子的尺寸。 在以下 $N$ 行中，每一行有 $M$ 个符号 `\` 或 `/`，表示连接对应电路元件对角线的导线的方向。
#### 输出格式：
如果可以打开灯，那么输出只包含一个整数，表示最少转动电路元件的数量。

如果不可能打开灯，输出 `NO SOLUTION`。

## 题目描述

Casper is designing an electronic circuit on a $N \times M$ rectangular grid plate. There are $N \times M$ square tiles that are aligned to the grid on the plate. Two (out of four) opposite corners of each tile are connected by a wire.

A power source is connected to the top left corner of the plate. A lamp is connected to the bottom right corner of the plate. The lamp is on only if there is a path of wires connecting power source to lamp. In order to switch the lamp on, any number of tiles can be turned by 90° (in both directions).

In the picture above the lamp is off. If any one of the tiles in the second column from the right is turned by 90° , power source and lamp get connected, and the lamp is on.

Write a program to find out the minimal number of tiles that have to be turned by 90° to switch the lamp on.

## 输入格式

The first line of input contains two integer numbers $N$ and $M$, the dimensions of the plate. In each of the following $N$ lines there are $M$ symbols – either \ or / – which indicate the direction of the wire connecting the opposite vertices of the corresponding tile.

## 输出格式

There must be exactly one line of output. If it is possible to switch the lamp on, this line must contain only one integer number: the minimal number of tiles that have to be turned to switch on the lamp. If it is not possible, output the string: ``NO SOLUTION``

## 样例 #1

### 样例输入 #1

```
3 5
\\/\\
\\///
/\\\\
```

### 样例输出 #1

```
1
```

## 提示

对于 $40\%$ 的数据，$1 \le N \le 4$，$1 \le M \le 5$。

对于所有数据，$1 \le N,M \le 500$。





## 分析过程：

![678b5307eba77a000000016c](C:\Users\Tomorrowland\AppData\Roaming\Tick_Tick\Image\678b5307eba77a000000016c.png)

![678b57a6eba77a0000000195](C:\Users\Tomorrowland\AppData\Roaming\Tick_Tick\Image\678b57a6eba77a0000000195.png)

## 代码:

```cpp
#include<bits/stdc++.h>
using namespace std;
const int N=510;
typedef pair<int,int> PII;
int dist[N][N];
bool vis[N][N];
char g[N][N];
int dx[]={-1,-1,1,1},dy[]={-1,1,1,-1};
int ex[]={-1,-1,0,0},ey[]={-1,0,0,-1};
char es[]="\\/\\/";
int n,m;
deque<PII> q;
int bfs()
{
    memset(dist,0x3f,sizeof dist);
    dist[0][0]=0;
    q.push_front({0,0});
    while(q.size()){
        auto u=q.front();q.pop_front();
        int x=u.first,y=u.second;
        if(vis[x][y]) continue;
        vis[x][y]=1;
        for(int i=0;i<4;i++){
            int a=x+dx[i],b=y+dy[i];
            if(a<0||a>n||b<0||b>m) continue;
            int ea=x+ex[i],eb=y+ey[i];
            int d=dist[x][y]+(g[ea][eb]!=es[i]);
            if(d>dist[a][b]) continue;
            dist[a][b]=d;
            if(g[ea][eb]==es[i]) q.push_front({a,b});
            else q.push_back({a,b});
        }
    }
    return dist[n][m];
}
int main()
{
    cin>>n>>m;
    for(int i=0;i<n;i++) cin>>g[i];
    int d=bfs();
    if(d==0x3f3f3f3f) cout<<"NO SOLUTION\n";
    else cout<<d<<'\n';
    return 0;
}
```

