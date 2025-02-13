# 216.组合总和III

[力扣题目链接(opens new window)](https://leetcode.cn/problems/combination-sum-iii/)

找出所有相加之和为 n 的 k 个数的组合。组合中只允许含有 1 - 9 的正整数，并且每种组合中不存在重复的数字。

说明：

+ 所有数字都是正整数。
+ 解集不能包含重复的组合。

示例 1: 输入: k = 3, n = 7 输出: [[1,2,4]]

示例 2: 输入: k = 3, n = 9 输出: [[1,2,6], [1,3,5], [2,3,4]]

## 思路

本题就是在[1,2,3,4,5,6,7,8,9]这个集合中找到和为n的k个数的组合。

相对于[77. 组合 (opens new window)](https://programmercarl.com/0077.组合.html)，无非就是多了一个限制，本题是要找到和为n的k个数的组合，而整个集合已经是固定的了[1,...,9]。

想到这一点了，做过[77. 组合 (opens new window)](https://programmercarl.com/0077.组合.html)之后，本题是简单一些了。

本题k相当于树的深度，9（因为整个集合就是9个数）就是树的宽度。

例如 k = 2，n = 4的话，就是在集合[1,2,3,4,5,6,7,8,9]中求 k（个数） = 2, n（和） = 4的组合。

选取过程如图：

![216.组合总和III](https://code-thinking-1253855093.file.myqcloud.com/pics/20201123195717975.png)

如图： ![216.组合总和III](https://code-thinking-1253855093.file.myqcloud.com/pics/20201123195717975-20230310113546003.png)

参照[关于回溯算法，你该了解这些！ (opens new window)](https://programmercarl.com/回溯算法理论基础.html)中的模板，不难写出如下C++代码：

```cpp
class Solution {
public:
    vector<int> path;
    vector<vector<int> > result;
    int sum=0;
    void dfs(int k,int n,int idx){
        if(path.size()==k){
            if(sum==n) result.push_back(path);
            return;
        }
        for(int i=idx;i<=9;i++){
            sum+=i;
            path.push_back(i);
            dfs(k,n,i+1);
            sum-=i;
            path.pop_back();
        }
    }
    vector<vector<int>> combinationSum3(int k, int n) {
        dfs(k,n,1);
        return result;
    }
};
```

## 剪枝：

```cpp
class Solution {
public:
    vector<int> path;
    vector<vector<int> > result;
    int sum=0;
    void dfs(int k,int n,int idx){
        if(path.size()==k){
            if(sum==n) result.push_back(path);
            return;
        }
        for(int i=idx;i<=9-(k-path.size())+1;i++){
            sum+=i;
            path.push_back(i);
            dfs(k,n,i+1);
            sum-=i;
            path.pop_back();
        }
    }
    vector<vector<int>> combinationSum3(int k, int n) {
        dfs(k,n,1);
        return result;
    }
};
```

