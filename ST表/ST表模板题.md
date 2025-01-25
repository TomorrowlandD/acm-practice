# 1.【模板】ST 表 && RMQ 问题

https://www.luogu.com.cn/problem/P3865

题目背景

这是一道 ST 表经典题——静态区间最大值

**请注意最大数据时限只有 0.8s，数据强度不低，请务必保证你的每次查询复杂度为 $O(1)$。若使用更高时间复杂度算法不保证能通过。**

如果您认为您的代码时间复杂度正确但是 TLE，可以尝试使用快速读入：

```cpp
inline int read()
{
	int x=0,f=1;char ch=getchar();
	while (ch<'0'||ch>'9'){if (ch=='-') f=-1;ch=getchar();}
	while (ch>='0'&&ch<='9'){x=x*10+ch-48;ch=getchar();}
	return x*f;
}
```

函数返回值为读入的第一个整数。

**快速读入作用仅为加快读入，并非强制使用。**

### 题目描述

给定一个长度为 $N$ 的数列，和 $ M $ 次询问，求出每一次询问的区间内数字的最大值。

### 输入格式

第一行包含两个整数 $N,M$，分别表示数列的长度和询问的个数。

第二行包含 $N$ 个整数（记为 $a_i$），依次表示数列的第 $i$ 项。

接下来 $M$ 行，每行包含两个整数 $l_i,r_i$，表示查询的区间为 $[l_i,r_i]$。

### 输出格式

输出包含 $M$ 行，每行一个整数，依次表示每一次询问的结果。

### 样例 #1

### 样例输入 #1

```
8 8
9 3 1 7 5 6 0 8
1 6
1 5
2 7
2 6
1 8
4 8
3 7
1 8
```

### 样例输出 #1

```
9
9
7
7
9
8
7
9
```

### 提示

对于 $30\%$ 的数据，满足 $1\le N,M\le 10$。

对于 $70\%$ 的数据，满足 $1\le N,M\le {10}^5$。

对于 $100\%$ 的数据，满足 $1\le N\le {10}^5$，$1\le M\le 2\times{10}^6$，$a_i\in[0,{10}^9]$，$1\le l_i\le r_i\le N$。

### 代码：

```cpp
#include<bits/stdc++.h>
using namespace std;
const int N=1e5+10;
int f[N][22];
int a[N];
int n,m;
void buildST()
{
    for(int i=1;i<=n;i++) f[i][0]=a[i];
    // 预处理，外层循环枚举区间长度，内存循环枚举左端点
    for(int j=1;j<=20;j++){
        for(int i=1;i+(1<<j)-1<=n;i++){
            //存区间最大值。
            f[i][j]=max(f[i][j-1],f[i+(1<<(j-1))][j-1]);
        } 
    }
}
int main()
{
    cin>>n>>m;
    for(int i=1;i<=n;i++) cin>>a[i];
    //构建ST表
    buildST();
    //查询区间最小值
    for(int i=1;i<=m;i++){
        int l,r;
        cin>>l>>r;
        int k=log2(r-l+1);
        cout<<max(f[l][k],f[r+1-(1<<k)][k])<<'\n';
    }
    return 0;
}
```

# 2.忠诚

https://www.luogu.com.cn/problem/P1816

### 题目描述

老管家是一个聪明能干的人。他为财主工作了整整  $10$ 年。财主为了让自已账目更加清楚，要求管家每天记  $k$ 次账。由于管家聪明能干，因而管家总是让财主十分满意。但是由于一些人的挑拨，财主还是对管家产生了怀疑。于是他决定用一种特别的方法来判断管家的忠诚，他把每次的账目按  $1, 2, 3 \ldots$ 编号，然后不定时的问管家问题，问题是这样的：在   $a$ 到  $b$ 号账中最少的一笔是多少？为了让管家没时间作假，他总是一次问多个问题。

### 输入格式

输入中第一行有两个数  $m, n$，表示有  $m$ 笔账  $n$ 表示有  $n$ 个问题。

第二行为  $m$ 个数，分别是账目的钱数。

后面  $n$ 行分别是  $n$ 个问题，每行有   $2$ 个数字说明开始结束的账目编号。

### 输出格式

在一行中输出每个问题的答案，以一个空格分割。

### 样例 #1

### 样例输入 #1

```
10 3
1 2 3 4 5 6 7 8 9 10
2 7
3 9
1 10
```

### 样例输出 #1

```
2 3 1
```

### 提示

对于 $100\%$ 的数据，$m \leq 10^5$，$n \leq 10^5$。

### 代码：

```cpp
#include<bits/stdc++.h>
using namespace std;
const int N=1e5+10;
int a[N];
int f[N][22];
int n,m;
void buildST()
{
    for(int i=1;i<=n;i++) f[i][0]=a[i];
    //外层循环枚举区间长度，内层循环枚举区间左端点
    for(int j=1;j<=20;j++){
        //内层循环条件为：右端点不超过边界n。
        for(int i=1;i-1+(1<<j)<=n;i++){
            f[i][j]=min(f[i][j-1],f[i+(1<<j-1)][j-1]);
        }
    }
}
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(0);cout.tie(0);
    cin>>n>>m;
    for(int i=1;i<=n;i++) cin>>a[i];
    buildST();
    for(int i=1;i<=m;i++){
        int l,r;cin>>l>>r;
        int k=log2(r-l+1);
        cout<<min(f[l][k],f[r+1-(1<<k)][k])<<' ';
    }
    return 0;
}
```

# 3.质量检测

https://www.luogu.com.cn/problem/P2251

### 题目描述

为了检测生产流水线上总共 $N$ 件产品的质量，我们首先给每一件产品打一个分数 $A$ 表示其品质，然后统计前 $M$ 件产品中质量最差的产品的分值 $Q[m] = min\{A_1, A_2, ... A_m\}$，以及第 2 至第 $M + 1$ 件的 $Q[m + 1], Q[m + 2] $... 最后统计第 $N - M + 1$ 至第 $N$ 件的 $Q[n]$。根据 $Q$ 再做进一步评估。

请你尽快求出 $Q$ 序列。

### 输入格式

输入共两行。

第一行共两个数 $N$、$M$，由空格隔开。含义如前述。

第二行共 $N$ 个数，表示 $N$ 件产品的质量。

### 输出格式

输出共 $N - M + 1$ 行。

第 1 至 $N - M + 1$ 行每行一个数，第 $i$ 行的数 $Q[i + M - 1]$。含义如前述。

### 样例 #1

### 样例输入 #1

```
10 4
16 5 6 9 5 13 14 20 8 12
```

### 样例输出 #1

```
5
5
5
5
5
8
8
```

### 提示

[数据范围]

30%的数据，$N \le 1000$

100%的数据，$N \le 100000$

100%的数据，$M \le N, A \le 1 000 000$

### 代码：

```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long
const int N=1e5+10;
int a[N];
int f[N][22];
int n,m;
void buildST()
{
    for(int i=1;i<=n;i++) f[i][0]=a[i];
    //外层循环枚举区间长度，内层循环枚举区间左端点
    for(int j=1;j<=20;j++){
        //内层循环条件为：右端点不超过边界n。
        for(int i=1;i-1+(1<<j)<=n;i++){
            f[i][j]=min(f[i][j-1],f[i+(1<<j-1)][j-1]);
        }
    }
}
signed main()
{
    ios::sync_with_stdio(false);
    cin.tie(0);cout.tie(0);
    cin>>n>>m;
    for(int i=1;i<=n;i++) cin>>a[i];
    buildST();
    int k=log2(m);
    for(int i=1;i<=n-m+1;i++){
        cout<<min(f[i][k],f[m+i-(1<<k)][k])<<'\n';
    }
    return 0;
}
```

