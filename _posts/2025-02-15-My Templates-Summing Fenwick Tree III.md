# 蒟蒻 tallnut 的模板库 - 求和树状数组（区间修改、区间查询）

## [返回模板库目录](https://tallnutliu.github.io/github-pages/2025/02/15/My-Templates-(Chinese-version).html)

## 功能
这个类实现了区间修改和区间查询的求和超级树状数组功能。

## 使用方式：
- 定义：`fenwick3<N,T> name;`
  
  （其中 `N` 表示树状数组要存储的元素个数，`T` 表示树状数组存储的类型（例如 `long long`，`double`））
  
- 初始化：`name.build(arr);`
  
  （其中 `arr` 表示原始数组）
  
- 单点修改（单点加上一个数）：`name.modify1(k,x);`
  
  （其中 `k` 表示元素下标，`x` 表示要加上的数）
  
- 单点查询（获取单点的值）：`name.query1(k)`

  （其中 `k` 表示要查询的下标）
  
- 区间修改（区间加上一个数）：`name.modify2(l,r,x);`
  
  （其中 `l,r` 表示该闭区间的左端点和右端点，`x` 表示加上的数）
  
- 区间查询（获取区间的和）：`name.query2(l,r)`
  
  （其中 `l,r` 表示该闭区间的左端点和右端点）

## 代码所需头文件
```cpp
#include <cstring>
```

## 代码
```cpp
namespace tallnut
{
	template <int N,typename T>
	class fenwick3
	{
		private:
			T a[N],d1[N],d2[N];
			int lowbit(int k) { return (k & (-k)); }
			void add(T arr[],int k,T x)
			{
				for (int i = k;i < N;i += lowbit(i))
					arr[i] += x;
			}
			T s(T arr[],int k)
			{
				T ans = 0;
				for (int i = k;i > 0;i -= lowbit(i))
					ans += arr[i];
				return ans;
			}
			T q(int k) { return s(d1,k) * (k + 1) - s(d2,k); }
		public:
			fenwick3()
			{
				memset(a,0,sizeof a);
				memset(d1,0,sizeof d1);
				memset(d2,0,sizeof d2);
			}
			void build(T arr[])
			{
				for (int i = 1;i < N;i++)
					modify1(i,arr[i]);
			}
			void modify1(int k,T x) { modify2(k,k,x); }
			T query1(int k) { return query2(k,k); }
			void modify2(int l,int r,T x)
			{
				add(d1,l,x);
				add(d1,r + 1,-x);
				add(d2,l,x * l);
				add(d2,r + 1,-x * (r + 1));
			}
			T query2(int l,int r) { return q(r) - q(l - 1); }
	};
}
```

## 压行版代码
```cpp
namespace tallnut{template<int N,typename T>class fenwick3{private:T a[N],d1[N],d2[N];int lowbit(int k){return(k&(-k));}void add(T arr[],int k,T x){for(int i=k;i<N;i+=lowbit(i))arr[i]+=x;}T s(T arr[],int k){T ans=0;for(int i=k;i>0;i-=lowbit(i))ans+=arr[i];return ans;}T q(int k){return s(d1,k)*(k+1)-s(d2,k);}public:fenwick3(){memset(a,0,sizeof a);memset(d1,0,sizeof d1);memset(d2,0,sizeof d2);}void build(T arr[]){for(int i=1;i<N;i++)modify1(i,arr[i]);}void modify1(int k,T x){modify2(k,k,x);}T query1(int k){return query2(k,k);}void modify2(int l,int r,T x){add(d1,l,x);add(d1,r+1,-x);add(d2,l,x*l);add(d2,r+1,-x*(r+1));}T query2(int l,int r){return q(r)-q(l-1);}};}
```
