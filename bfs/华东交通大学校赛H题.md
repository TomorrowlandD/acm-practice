https://ac.nowcoder.com/acm/contest/93820/H

![image-20250118133750575](C:\Users\Tomorrowland\AppData\Roaming\Typora\typora-user-images\image-20250118133750575.png)

![image-20250118133822958](C:\Users\Tomorrowland\AppData\Roaming\Typora\typora-user-images\image-20250118133822958.png)

![image-20250118133834531](C:\Users\Tomorrowland\AppData\Roaming\Typora\typora-user-images\image-20250118133834531.png)



### 代码：

本题为bfs模板题，直接将起点1入队，然后洪水覆盖即可。

```cpp
#include<bits/stdc++.h>
using namespace std;
const int N=1e5+10;
int dist[N],a[N];
int n;
void solve()
{
    cin>>n;
    for(int i=1;i<=n;i++) cin>>a[i];
    fill(dist,dist+N,-1);
    dist[1]=0;
    queue<int> q;
    q.push(1);
    while(q.size()){
        auto u=q.front();q.pop();
        if(u+a[u]<=n&&dist[u+a[u]]==-1) {q.push(u+a[u]);dist[u+a[u]]=dist[u]+1;}
        if(u-a[u]>=1&&dist[u-a[u]]==-1) {q.push(u-a[u]);dist[u-a[u]]=dist[u]+1;}
        if(u+1<=n&&dist[u+1]==-1) {q.push(u+1);dist[u+1]=dist[u]+1;}
        if(u-1>=1&&dist[u-1]==-1) {q.push(u-1);dist[u-1]=dist[u]+1;}
        if(u+1==n||u-1==n||u-a[u]==n||u+a[u]==n){
            cout<<dist[n]<<'\n';
            return;
        }
    }
}
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(0);cout.tie(0);
    int t=1;cin>>t;
    while(t--) solve();
    return 0;
}
```

