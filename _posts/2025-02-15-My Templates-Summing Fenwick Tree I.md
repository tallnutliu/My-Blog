# 蒟蒻 tallnut 的模板库 - 求和树状数组（单点修改、区间查询）

## [返回模板库目录](https://tallnutliu.github.io/My-Blog/2025/02/15/My-Templates-(Chinese-version).html)

## 功能
这个类实现了单点修改和区间求和树状数组功能。

## 使用方式
- 定义：`fenwick1<N,T> name;`
  
  （其中 `N` 表示树状数组要存储的元素个数，`T` 表示树状数组存储的类型（例如 `long long`，`double`））
  
- 初始化：`name.build(arr);`
  
  （其中 `arr` 表示原始数组）
  
- 单点修改（单点加上一个数）：`name.modify(k,x);`
  
  （其中 `k` 表示元素下标，`x` 表示要加上的数）
  
- 区间查询（获取区间的和）：`name.query(l,r)`
  
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
	class fenwick1
	{
		private:
			T a[N];
			int lowbit(int k) { return (k & (-k)); }
			T s(int k)
			{
				T ans = 0;
				for (int i = k;i > 0;i -= lowbit(i))
					ans += a[i];
				return ans;
			}
		public:
			fenwick1() { memset(a,0,sizeof a); }
			void build(T arr[])
			{
				for (int i = 1;i < N;i++)
					modify(i,arr[i]);
			}
			T query(int l,int r) { return s(r) - s(l - 1); }
			void modify(int k,T x)
			{
				for (int i = k;i < N;i += lowbit(i))
					a[i] += x;
			}
	};
}
```

## 压行版代码
```cpp
namespace tallnut{template<int N,typename T>class fenwick1{private:T a[N];int lowbit(int k){return(k&(-k));}T s(int k){T ans=0;for(int i=k;i>0;i-=lowbit(i))ans+=a[i];return ans;}public:fenwick1(){memset(a,0,sizeof a);}void build(T arr[]){for(int i=1;i<N;i++)modify(i,arr[i]);}T query(int l,int r){return s(r)-s(l-1);}void modify(int k,T x){for(int i=k;i<N;i+=lowbit(i))a[i]+=x;}};}
```
