![img](https://img2024.cnblogs.com/blog/3476421/202501/3476421-20250124223758330-1943682220.png)

![](https://img2024.cnblogs.com/blog/3476421/202502/3476421-20250212223009858-1434595697.png)

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

