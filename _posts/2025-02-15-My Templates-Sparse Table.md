# 蒟蒻 tallnut 的模板库 - ST 表
## [返回模板库目录](https://tallnutliu.github.io/github-pages/2025/02/15/My-Templates-(Chinese-version).html)
## 功能
这个类实现了求解 RMQ 问题的 ST 表功能。
## 使用方式
- 定义：`ST<N,T> name;`
  
  （其中 `N` 表示 ST 表要处理的元素个数，`T` 表示 ST 表存储的类型（如 `int`，`long long`））
  
- 初始化：`name.build(arr);`
  
  （其中 `arr` 表示原始数组）
  
- 区间查询（获取区间最大值）：`name.query(l,r)`
  
  （其中 `l,r` 表示该区间的左端点和右端点）
## 代码所需头文件
```cpp
#include <cstring>
```
## 代码
```cpp
namespace tallnut
{
    template <int N,typename T>
    class ST
    {
        private:
            T st[N][20];
            int lg[N];
        public:
            ST()
            {
                memset(lg,0,sizeof(lg));
                memset(st,0,sizeof(st));
            }
            void build(T arr[])
            {
                for (int i = 1;i < N;i++)
                    st[i][0] = arr[i];
                for (int i = 2;i < N;i++)
                    lg[i] = lg[i >> 1] + 1;
                for (int j = 1;j <= lg[N - 1];j++)
                    for (int i = 1;i + (1 << j) - 1 < N;i++)
                        st[i][j] = max(st[i][j - 1],st[i + (1 << (j - 1))][j - 1]);
            }
            T query(int l,int r)
            {
                int k = lg[r - l + 1];
                return max(st[l][k],st[r - (1 << k) + 1][k]);
            }
    };
}
```
## 压行版代码
```cpp
namespace tallnut{template<int N,typename T>class ST{private:T st[N][20];int lg[N];public:ST(){memset(lg,0,sizeof(lg));memset(st,0,sizeof(st));}void build(T arr[]){for(int i=1;i<N;i++)st[i][0]=arr[i];for(int i=2;i<N;i++)lg[i]=lg[i>>1]+1;for(int j=1;j<=lg[N-1];j++)for(int i=1;i+(1<<j)-1<N;i++)st[i][j]=max(st[i][j-1],st[i+(1<<(j-1))][j-1]);}T query(int l,int r){int k=lg[r-l+1];return max(st[l][k],st[r-(1<<k)+1][k]);}};}
```
