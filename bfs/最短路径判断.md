# Obsession with Robots

https://codeforces.com/problemset/problem/8/B

## 题面翻译

有一个机器人在一个无穷大的网格上，网格中有些格子机器人无法通过而剩下的可以。现在给出了他的路径，`UDLR` 分别表示往上下左右走 $1$ 个单位长。请判断是否存在一个网格，使得机器人的这个路径合法，且为这个网格中起点到终点的最短路径。如果存在输出 `OK`，否则输出 `BUG`。

输入字符串长度不超过 $100$。

## 题目描述

The whole world got obsessed with robots,and to keep pace with the progress, great Berland's programmer Draude decided to build his own robot. He was working hard at the robot. He taught it to walk the shortest path from one point to another, to record all its movements, but like in many Draude's programs, there was a bug — the robot didn't always walk the shortest path. Fortunately, the robot recorded its own movements correctly. Now Draude wants to find out when his robot functions wrong. Heh, if Draude only remembered the map of the field, where he tested the robot, he would easily say if the robot walked in the right direction or not. But the field map was lost never to be found, that's why he asks you to find out if there exist at least one map, where the path recorded by the robot is the shortest.

The map is an infinite checkered field, where each square is either empty, or contains an obstruction. It is also known that the robot never tries to run into the obstruction. By the recorded robot's movements find out if there exist at least one such map, that it is possible to choose for the robot a starting square (the starting square should be empty) such that when the robot moves from this square its movements coincide with the recorded ones (the robot doesn't run into anything, moving along empty squares only), and the path from the starting square to the end one is the shortest.

In one movement the robot can move into the square (providing there are no obstrutions in this square) that has common sides with the square the robot is currently in.

## 输入格式

The first line of the input file contains the recording of the robot's movements. This recording is a non-empty string, consisting of uppercase Latin letters L, R, U and D, standing for movements left, right, up and down respectively. The length of the string does not exceed 100.

## 输出格式

In the first line output the only word OK (if the above described map exists), or BUG (if such a map does not exist).

## 样例 #1

### 样例输入 #1

```
LLUUUR
```

### 样例输出 #1

```
OK
```

## 样例 #2

### 样例输入 #2

```
RRUULLDD
```

### 样例输出 #2

```
BUG
```





## 思路：

在广度优先搜索（BFS）中，如果除了走过来的那个点以外，其它三个点有走过的话，就一定不是最优解，原因主要有以下几点： **一、BFS 的性质** BFS 是一种逐层搜索的算法，它从起始点开始，先搜索距离起始点为 1 的所有节点，然后是距离为 2 的节点，以此类推。这意味着在 BFS 过程中，首次找到的到达某个节点的路径一定是最短路径。 **二、非最优情况分析** 1. 对于当前位置，如果除了走过来的那个格子以外，周围还有其他被走过的格子，这就违背了 BFS 的最短路径特性。   - 因为如果按照最优路径前进，在某一时刻到达一个特定位置时，周围的格子应该都是未被访问过的，只有这样才能保证是沿着最短路径到达该位置。   - 如果周围有其他被走过的格子，说明之前可能有其他路径已经经过了这些格子，而当前路径不是第一个到达这里的，也就不是最短路径。 2. 从直观上来说，想象在一个迷宫中进行 BFS，每次都是从距离起始点最近的未访问过的格子开始探索。如果当前位置周围有多个已经被走过的格子，那就意味着有其他路径在更早的时候就到达了这些周围的格子，而当前路径却在较晚的时候才到达，显然不是最优的。 综上所述，在 BFS 中，如果出现除了走过来的那个点以外其它三个点有走过的情况，就可以判断不是最优解。

## 代码：

```cpp
#include<iostream>
#include<cstring>
using namespace std;
bool vis[205][205];
string s;
int sx = 101, sy = 101;
int dx[]{ -1,0,1,0 };
int dy[]{ 0,1,0,-1 };
bool check(int x, int y) {
	if (vis[x][y]) return false;
	int cnt = 0;
	for (int i = 0; i < 4; i++) {
		int a = x + dx[i];
		int b = y + dy[i];
		cnt += vis[a][b];
	}
	return cnt <= 1;
}
int main()
{
	cin >> s;
	for (int i = 0; i < s.size(); i++) {
		vis[sx][sy] = 1;
		if (s[i] == 'L') {
			sy--;
			if (!check(sx, sy)) { cout << "BUG" << endl; return 0; }
		}
		if (s[i] == 'R') {
			sy++;
			if (!check(sx, sy)) { cout << "BUG" << endl; return 0; }
		}
		if (s[i] == 'U') {
			sx--;
			if (!check(sx, sy)) { cout << "BUG" << endl; return 0; }
		}
		if (s[i] == 'D') {
			sx++;
			if (!check(sx, sy)) { cout << "BUG" << endl; return 0; }
		}
	}
	cout << "OK" << endl;
	return 0;
}
```

