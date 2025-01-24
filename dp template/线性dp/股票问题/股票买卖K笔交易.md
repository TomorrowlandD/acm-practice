https://www.acwing.com/problem/content/1059/

![img](https://img2024.cnblogs.com/blog/3476421/202501/3476421-20250124001819470-457664393.png)

上图的利润为8，不是9。图中标错了。

![img](https://img2024.cnblogs.com/blog/3476421/202501/3476421-20250124010139007-484903430.png)

![img](https://img2024.cnblogs.com/blog/3476421/202501/3476421-20250124010543001-664567038.png)

## 代码：

```cpp
#include<bits/stdc++.h>
using namespace std;
const int N=1e3+10;
int w[N],dp[N][N][2];
int main()
{
    ios::sync_with_stdio(false);
    cout.tie(0);cout.tie(0);
    int n,k;cin>>n>>k;
    for(int i=1;i<=n;i++) cin>>w[i];
    for(int j=1;j<=k;j++) dp[0][j][1]=-1e9;
    for(int i=1;i<=n;i++){
        for(int j=1;j<=k;j++){
            dp[i][j][0]=max(dp[i-1][j][0],dp[i-1][j][1]+w[i]);
            dp[i][j][1]=max(dp[i-1][j-1][0]-w[i],dp[i-1][j][1]);
        }
    }
    cout<<dp[n][k][0];
    return 0;
}
```



若是两笔交易，则：

```cpp
#include<bits/stdc++.h>
using namespace std;
const int N=1e5+10;
#define int long long
int w[N],dp[N][3][2];
signed main()
{
    ios::sync_with_stdio(false);
    cout.tie(0);cout.tie(0);
    int n;cin>>n;
    for(int i=1;i<=n;i++) cin>>w[i];
    for(int j=1;j<=2;j++) dp[0][j][1]=-1e11;
    for(int i=1;i<=n;i++){
        for(int j=1;j<=2;j++){
            dp[i][j][0]=max(dp[i-1][j][0],dp[i-1][j][1]+w[i]);
            dp[i][j][1]=max(dp[i-1][j-1][0]-w[i],dp[i-1][j][1]);
        }
    }
    cout<<dp[n][2][0];
    return 0;
}
```



