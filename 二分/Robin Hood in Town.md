# Robin Hood in Town

https://codeforces.com/problemset/problem/2014/C

## 题面翻译

在舍伍德，我们评判一个人不是看他的财富，而是看他的功绩。

环顾四周，富人越来越富，穷人越来越穷。我们需要取富济贫。我们需要罗宾汉

镇上住着 $n$ 人。刚才， $i$ 每个人的财富是 $a_i$ 金子。但你猜怎么着？最富有的人又找到了一罐金子

更正式地说，找到一个 $a_j=max(a_1, a_2, \dots, a_n)$ ，把 $a_j$ 改成 $a_j+x$ ，其中 $x$ 是在锅里找到的黄金的非负整数。如果有多个最大值，则可以是其中任意一个。

如果一个人的财富**严格少于平均财富 $^{\text{∗}}$ 的一半，那么这个人就是不快乐的。

如果**严格来说超过总人口 $n$ 的一半，那么罗宾汉就会应大众的要求出现。

求罗宾汉出现的最小值 $x$ ，如果不可能，则输出 $-1$ 。

$^{\text{∗}}$ 平均财富的定义是总财富除以总人口 $n$ ，即 $\frac{\sum a_i}{n}$ ，结果为实数 。

**输入**

第一行输入包含一个整数 $t$ ( $1 \le t \le 10^4$ ) - 测试用例数。

每个测试用例的第一行包含一个整数 $n$ ( $1 \le n \le 2\cdot10^5$ ) - 总人数。

每个测试用例的第二行包含 $n$ 个整数 $a_1, a_2, \ldots, a_n$ ( $1 \le a_i \le 10^6$ ) --每个人的财富。

保证所有测试用例中 $n$ 的总和不超过 $2 \cdot 10^5$ 。

**输出**

对于每个测试用例，输出一个整数 - 最富有的人必须找到的最少黄金数量，罗宾汉才会出现。如果不可能，则输出 $-1$ 。

**注**

在第一个测试案例中，不可能只有一个人不快乐。

在第二种情况下，总有 $1$ 个快乐的人（最富有的人）。

在第三种情况下，不需要额外的黄金，所以答案是 $0$ 。

在第四种测试情形中，增加 $15$ 黄金后，平均财富变为 $\frac{25}{4}$ ，而这个平均值的一半是 $\frac{25}{8}$ ，结果是 $3$ 人不快乐。

在第五个测试案例中，加入 $16$ 黄金后，平均财富变为 $\frac{31}{5}$ ，导致 $3$ 人不快乐。

## 题目描述

In Sherwood, we judge a man not by his wealth, but by his merit.



Look around, the rich are getting richer, and the poor are getting poorer. We need to take from the rich and give to the poor. We need Robin Hood!

There are $ n $ people living in the town. Just now, the wealth of the $ i $ -th person was $ a_i $ gold. But guess what? The richest person has found an extra pot of gold!

More formally, find an $ a_j=max(a_1, a_2, \dots, a_n) $ , change $ a_j $ to $ a_j+x $ , where $ x $ is a non-negative integer number of gold found in the pot. If there are multiple maxima, it can be any one of them.

A person is unhappy if their wealth is strictly less than half of the average wealth $ ^{\text{∗}} $ .

If strictly more than half of the total population $ n $ are unhappy, Robin Hood will appear by popular demand.

Determine the minimum value of $ x $ for Robin Hood to appear, or output $ -1 $ if it is impossible.

 $ ^{\text{∗}} $ The average wealth is defined as the total wealth divided by the total population $ n $ , that is, $ \frac{\sum a_i}{n} $ , the result is a real number.

## 输入格式

The first line of input contains one integer $ t $ ( $ 1 \le t \le 10^4 $ ) — the number of test cases.

The first line of each test case contains an integer $ n $ ( $ 1 \le n \le 2\cdot10^5 $ ) — the total population.

The second line of each test case contains $ n $ integers $ a_1, a_2, \ldots, a_n $ ( $ 1 \le a_i \le 10^6 $ ) — the wealth of each person.

It is guaranteed that the sum of $ n $ across all test cases does not exceed $ 2 \cdot 10^5 $ .

## 输出格式

For each test case, output one integer — the minimum number of gold that the richest person must find for Robin Hood to appear. If it is impossible, output $ -1 $ instead.

## 样例 #1

### 样例输入 #1

```
6
1
2
2
2 19
3
1 3 20
4
1 2 3 4
5
1 2 3 4 5
6
1 2 1 1 1 25
```

### 样例输出 #1

```
-1
-1
0
15
16
0
```

## 提示

In the first test case, it is impossible for a single person to be unhappy.

In the second test case, there is always $ 1 $ happy person (the richest).

In the third test case, no additional gold are required, so the answer is $ 0 $ .

In the fourth test case, after adding $ 15 $ gold, the average wealth becomes $ \frac{25}{4} $ , and half of this average is $ \frac{25}{8} $ , resulting in $ 3 $ people being unhappy.

In the fifth test case, after adding $ 16 $ gold, the average wealth becomes $ \frac{31}{5} $ , resulting in $ 3 $ people being unhappy.





## 思路：

这题有两种思路，一种是贪心的去想，另一种是二分的思路。

### 贪心做法：

我们要想，若罗宾汉出现，则“不快乐”的人一定至少是总人数的一半（向下取整）+1，假设我们所有人的总财富为sum，每个人的财富为`a[i]`，我们对财富进行排序以后，则一定有：`a[n/2+1]*2*n<sum`，（因为至少有一半+1的人不快乐），这里注意，我们一定不要使用除法，除法的四舍五入会丢失精度，碰到大数据时会出事。

如果说，我们原本的`a[n/2+1]*2*n<sum`就成立，那么我们不需要加钱。答案为0.

如果这个式子不成立的话，那么我们需要给最富的人找到一些钱，让这个式子成立。那么我们给多少钱呢？因为给的钱一定是整数，我们只需要让这个式子刚好成立，那么就是X的最小值，那么`x=a[n/2+1]*2*n-sum+1`。这里的临界条件就是：我给最富的人一些钱，刚好给到`a[n/2+1]*2*n==sum`，此时罗宾汉恰好不出现，我要使得罗宾汉出现，只需要再给一块钱，就能实现。这里需要好好钻研一下。

需要注意的是，当n的值<3时，罗宾汉一定不会出现，因为n=2，n=1。永远不会超过一半的人不快乐。

### 二分做法：

二分的做法其实和贪心也是比较相似的，先对数组进行排序，判断是否不需要加钱，罗宾汉就会自己出现。否则，就对需要加的钱数（X）进行二分，这里注意开的上界要大一点，这里的数据比较大。

### 贪心代码：

```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long 
const int N=2e5+10;
int a[N],n;
void solve()
{
    cin>>n;
    int sum=0;
    for(int i=1;i<=n;i++) cin>>a[i],sum+=a[i];
    if(n<=2){
        cout<<-1<<"\n";
        return;
    }
    sort(a+1,a+1+n);
    // if(a[n/2+1]*2*n<sum) ans=0;
     else ans=a[n/2+1]*2*n-sum+1;
    cout<<ans<<'\n'; 
}
signed main()
{
    ios::sync_with_stdio(false);
    cin.tie(0);cout.tie(0);
    int t=1;cin>>t;
    while(t--) solve();
}
```

### 二分代码:

```c++
#include<bits/stdc++.h>
using namespace std;
#define int long long 
const int N=2e5+10;
int a[N],n;
bool check(int x,int sum){
    sum+=x;
    if(a[n/2+1]*2*n<sum) return true;
    return false;
}
int find(int sum)
{
    int l=0,r=1e14+1;
    while(l+1<r){
        int mid=l+r>>1;
        if(check(mid,sum)) r=mid;
        else l=mid;
    }
    return r;
}
void solve()
{
    cin>>n;
    int sum=0;
    for(int i=1;i<=n;i++) cin>>a[i],sum+=a[i];
    if(n<=2){
        cout<<-1<<"\n";
        return;
    }
    sort(a+1,a+1+n);

    if(a[n/2+1]*2*n<sum) {
        cout<<0<<'\n';
        return;
    }
    cout<<find(sum)<<'\n'; 
}
signed main()
{
    ios::sync_with_stdio(false);
    cin.tie(0);cout.tie(0);
    int t=1;cin>>t;
    while(t--) solve();
}
```

