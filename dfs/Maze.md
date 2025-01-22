# Maze

http://codeforces.com/problemset/problem/377/A

## 题面翻译

题目描述：

小P非常的喜欢方格迷宫。方格迷宫是一个n*m的由墙和空地构成的长方形方阵。只有当两点满足四联通条件时才能走过去。

小P画了一个迷宫，里面所有的空地都是四连通的。但~~闲着没事干的~~小P认为自己画的迷宫里小墙太多了很难看，所以他希望能够通过把迷宫中k个格子从空地变成墙但不破坏整张图的连通性（即仍然保持所有空地在一个四连通块中）

但是小P太蠢了做不来，请你帮助他。

输入：
第一行n,m,k（描述如题）
第二到n+1行：
每行m个字符，分别是'.'或'#'。 '.'表示空地，'#'表示墙。
输出：
把整张图原样打出来，但是被你修改的格子输出'X'。

（题意基本正确）

## 题目描述

Pavel loves grid mazes. A grid maze is an $ n×m $ rectangle maze where each cell is either empty, or is a wall. You can go from one cell to another only if both cells are empty and have a common side.

Pavel drew a grid maze with all empty cells forming a connected area. That is, you can go from any empty cell to any other one. Pavel doesn't like it when his maze has too little walls. He wants to turn exactly $ k $ empty cells into walls so that all the remaining cells still formed a connected area. Help him.

## 输入格式

The first line contains three integers $ n $ , $ m $ , $ k $ ( $ 1<=n,m<=500 $ , $ 0<=k&lt;s $ ), where $ n $ and $ m $ are the maze's height and width, correspondingly, $ k $ is the number of walls Pavel wants to add and letter $ s $ represents the number of empty cells in the original maze.

Each of the next $ n $ lines contains $ m $ characters. They describe the original maze. If a character on a line equals ".", then the corresponding cell is empty and if the character equals "\#", then the cell is a wall.

## 输出格式

Print $ n $ lines containing $ m $ characters each: the new maze that fits Pavel's requirements. Mark the empty cells that you transformed into walls as "X", the other cells must be left without changes (that is, "." and "\#").

It is guaranteed that a solution exists. If there are multiple solutions you can output any of them.

## 样例 #1

### 样例输入 #1

```
3 4 2
#..#
..#.
#...
```

### 样例输出 #1

```
#.X#
X.#.
#...
```

## 样例 #2

### 样例输入 #2

```
5 4 5
#...
#.#.
.#..
...#
.#.#
```

### 样例输出 #2

```
#XXX
#X#.
X#..
...#
.#.#
```





## 思路：

简单来说，这段文字描述了一个解题思路，用于解决将迷宫中的一部分空格子变成障碍物，同时保证剩下的空格子仍然是连通的问题。主要思路是通过逆向思维，先将所有的空格子标记为障碍物，然后找到一个特定大小的障碍物区域，并将其恢复为空格子，确保剩下的空格子是连通的。整个过程涉及到深度优先搜索算法来实现。

## 代码：

```cpp
#include<cstdio>
int n, m, k, cnt;
char g[505][505];
int dx[]{ -1,0,1,0 };
int dy[]{ 0,1,0,-1 };
void dfs(int x, int y) {
	if (k <= 0) return;
	g[x][y] = '.';
	k--;
	for (int i = 0; i < 4; i++) {
		int a = x + dx[i];
		int b = y + dy[i];
		if (a >= 1 && a <= n && b >= 1 && b <= m && g[a][b] == 'X' && k) dfs(a, b);
	}
}
int main()
{
	scanf("%d%d%d", &n, &m, &k);
	for (int i = 1; i <= n; i++) {
		scanf("%s", g[i] + 1);
		for (int j = 1; j <= m; j++) {
			if (g[i][j] == '.') g[i][j] = 'X', cnt++;
		}
	}
	k = cnt - k;
	for (int i = 1; i <= n; i++) {
		for (int j = 1; j <= m; j++) {
			if (g[i][j] == 'X') {
				dfs(i, j);
				for (int t = 1; t <= n; t++) printf("%s\n", g[t] + 1);
				return 0;
			}
		}
	}
	return 0;
}
```

