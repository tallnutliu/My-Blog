# 蒟蒻 tallnut 的模板库 - 求和树状数组（区间修改、单点查询）
## [返回模板库目录](https://www.luogu.com.cn/paste/yw5teupm)
## 功能
这个类实现了区间修改和单点求值树状数组功能。
## 使用方式
- 定义：`fenwick2<N,T> name;`
  
  （其中 `N` 表示树状数组要存储的元素个数，`T` 表示树状数组存储的类型（例如 `long long`，`double`））
  
- 初始化：`name.build(arr);`
  
  （其中 `arr` 表示原始数组）
  
- 区间修改（区间加上一个数）：`name.modify(l,r,x);`
  
  （其中 `l,r` 表示该区间的左端点和右端点，`x` 表示要加上的数）
  
- 单点查询（获取单点的值）：`name.query(k)`
  
  （其中 `k` 表示元素下标）
## 代码所需头文件
```cpp
#include <cstring>
```
## 代码
```cpp
namespace tallnut
{
    template <int N,typename T>
    class fenwick2
    {
        private:
            T a[N];
            inline int lowbit(int x) { return x & (-x); }
            T s(int k)
            {
                T ans = 0;
                for (int i = k;i > 0;i -= lowbit(i))
                    ans += a[i];
                return ans;
            }
        public:
            fenwick2() { memset(a,0,sizeof(a)); }
            void build(T arr[])
            {
                for (int i = 1;i < N;i++)
                    modify(i,i,arr[i]);
            }
            T query(int k) { return s(k); }
            void modify(int l,int r,T x)
            {
                for (int i = l;i < N;i += lowbit(i))
                    a[i] += x;
                for (int i = r + 1;i < N;i += lowbit(i))
                    a[i] -= x;
            }
    };
}
```
## 压行版代码
```cpp
namespace tallnut{template<int N,typename T>class fenwick2{private:T a[N];inline int lowbit(int x){return x&(-x);}T s(int k){T ans=0;for(int i=k;i>0;i-=lowbit(i))ans+=a[i];return ans;}public:fenwick2(){memset(a,0,sizeof(a));}void build(T arr[]){for(int i=1;i<N;i++)modify(i,i,arr[i]);}T query(int k){return s(k);}void modify(int l,int r,T x){for(int i=l;i<N;i+=lowbit(i))a[i]+=x;for(int i=r+1;i<N;i+=lowbit(i))a[i]-=x;}};}
```
