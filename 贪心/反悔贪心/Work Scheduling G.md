# [USACO09OPEN] Work Scheduling G

https://www.luogu.com.cn/problem/P2949

## 题面翻译

约翰有太多的工作要做。为了让农场高效运转，他必须靠他的工作赚钱，每项工作花一个单位时间。 他的工作日从 $0$ 时刻开始，有 $10^9$ 个单位时间。在任一时刻，他都可以选择编号 $1$ 到 $N$ 的 $N(1 \leq N \leq 10^5)$ 项工作中的任意一项工作来完成。 因为他在每个单位时间里只能做一个工作，而每项工作又有一个截止日期，所以他很难有时间完成所有N个工作，虽然还是有可能。 对于第 $i$ 个工作，有一个截止时间 $D_i(1 \leq D_i \leq 10^9)$，如果他可以完成这个工作，那么他可以获利 $P_i( 1\leq P_i\leq 10^9 )$. 在给定的工作利润和截止时间下，约翰能够获得的利润最大为多少.

## 题目描述

Farmer John has so very many jobs to do! In order to run the farm efficiently, he must make money on the jobs he does, each one of which takes just one time unit.

His work day starts at time 0 and has 1,000,000,000 time units (!).  He currently can choose from any of N (1 <= N <= 100,000) jobs

conveniently numbered 1..N for work to do. It is possible but

extremely unlikely that he has time for all N jobs since he can only work on one job during any time unit and the deadlines tend to fall so that he can not perform all the tasks.

Job i has deadline D\_i (1 <= D\_i <= 1,000,000,000). If he finishes job i by then, he makes a profit of P\_i (1 <= P\_i <= 1,000,000,000).

What is the maximum total profit that FJ can earn from a given list of jobs and deadlines?  The answer might not fit into a 32-bit integer.

## 输入格式

\* Line 1: A single integer: N

\* Lines 2..N+1: Line i+1 contains two space-separated integers: D\_i and P\_i

## 输出格式

\* Line 1: A single number on a line by itself that is the maximum possible profit FJ can earn.

## 样例 #1

### 样例输入 #1

```
3 
2 10 
1 5 
1 7
```

### 样例输出 #1

```
17
```

## 提示

Complete job 3 (1,7) at time 1 and complete job 1 (2,10) at time 2 to maximize the earnings (7 + 10 -> 17).

## 思路：

反悔贪心：先对n项工作，按照截至日期排序。

然后枚举每项工作

如果当前工作有时间做，那么先做了它（贪心），并且把它的利润压入一个小根堆

如果当前工作与前项工作截至时间相同(`d[i]==q.size()`，就进一步比较，如果当前工作利润大于堆顶的工作利润，就放弃堆顶的那个工作（反悔），，用做它的时间去做当前工作，利润更大

