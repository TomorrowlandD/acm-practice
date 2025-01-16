

# Game with Doors

https://codeforces.com/problemset/problem/2004/B

## 题面翻译

### 题面描述
有 $100$ 个房间排成一列，之间有 $99$ 个门; 第 $i$ 个门连接第 $i$ 个房间和第 $i+1$ 个房间。每扇门可以上锁也可以不上锁。最初，所有的门都没有锁。

我们说，房间 $x$ 是可以到房间 $y$ 的，如果 $x$ 与 $y$ 之间的所有门都没锁。

你知道的:

- 爱丽丝在 $[l,r]$ 的某个房间里;
- Bob 在 $[L,R]$ 的某个房间里;
- 爱丽丝和鲍勃在不同的房间。

然而，你并不知道他们所在的确切房间。

你不希望爱丽丝和鲍勃能够联系到对方，所以你要锁上一些门来防止这种情况发生。无论 Alice 和 Bob 在给定段中的起始位置如何，您需要锁定的门的最小数量是多少？

### 输入格式
第一行包含单个整数 $t$ ( $1 \le t \le 10^4$ )ー测试用例的数量。

每个测试用例的第一行包含两个整数 $ l $ 和 $ r $ ( $ 1 \le l < r \le 100 $ ) ーー Alice 所在房间段。

每个测试用例的第二行包含两个整数 $ L $ 和 $ R $ ( $ 1 \le L < R \le 100 $ ) ーー Bob 所在房间段。

### 输出格式
对于每个测试用例，打印一个整数ーー必须锁定的门的最小数目，以便 Alice 和 Bob 不能相遇，而不管它们在给定段中的起始位置如何。

## 题目描述

There are $ 100 $ rooms arranged in a row and $ 99 $ doors between them; the $ i $ -th door connects rooms $ i $ and $ i+1 $ . Each door can be either locked or unlocked. Initially, all doors are unlocked.

We say that room $ x $ is reachable from room $ y $ if all doors between them are unlocked.

You know that:

- Alice is in some room from the segment $ [l, r] $ ;
- Bob is in some room from the segment $ [L, R] $ ;
- Alice and Bob are in different rooms.

However, you don't know the exact rooms they are in.

You don't want Alice and Bob to be able to reach each other, so you are going to lock some doors to prevent that. What's the smallest number of doors you have to lock so that Alice and Bob cannot meet, regardless of their starting positions inside the given segments?

## 输入格式

The first line contains a single integer $ t $ ( $ 1 \le t \le 10^4 $ ) — the number of test cases.

The first line of each test case contains two integers $ l $ and $ r $ ( $ 1 \le l < r \le 100 $ ) — the bounds of the segment of rooms where Alice is located.

The second line of each test case contains two integers $ L $ and $ R $ ( $ 1 \le L < R \le 100 $ ) — the bounds of the segment of rooms where Bob is located.

## 输出格式

For each test case, print a single integer — the smallest number of doors you have to lock so that Alice and Bob cannot meet, regardless of their starting positions inside the given segments.

## 样例 #1

### 样例输入 #1

```
4
1 2
3 4
2 5
2 5
3 7
6 7
4 5
2 8
```

### 样例输出 #1

```
1
3
2
3
```

## 提示

In the first test case, it is sufficient to lock the door between rooms $ 2 $ and $ 3 $ .

In the second test case, the following doors have to be locked: $ (2,3) $ , $ (3,4) $ , $ (4,5) $ .

In the third test case, the following doors have to be locked: $ (5, 6) $ and $ (6,7) $ .

## 思路：

不要上来直接分七八种情况然后分类讨论，要注意总结规律和套路。一眼看破这道题的本质。

我们这道题的本质其实就是找交叉区间的长度，同时注意它们有没有端点是重合的。

##  代码：

```c++
#include<bits/stdc++.h>
using namespace std;
#define IOS ios::sync_with_stdio(false);cin.tie(0);cout.tie(0);
void solve()
{
    int l,r;cin>>l>>r;
    int L,R;cin>>L>>R;
    int inter=min(r,R)-max(l,L)+1;
    if(inter<=0){
        cout<<1<<'\n';
        return;
    }
    int ans=inter-1;
    ans+=(l!=L);
    ans+=(r!=R);
    
    cout<<ans<<'\n';
}
int main()
{
    IOS;
    int t=1;cin>>t;
    while(t--) solve();
    return 0;
}
```

