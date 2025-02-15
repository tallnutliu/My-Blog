# 蒟蒻 tallnut 的模板库 - 求和线段树
## [返回模板库目录](https://tallnutliu.github.io/github-pages/2025/02/15/My-Templates-(Chinese-version).html)
## 功能
这个类实现了区间修改、求和线段树功能。
## 使用方式
- 定义：`segtree1<N,T> name;`
  
  （其中 `N` 表示线段树要存储的元素个数，`T` 表示线段树存储的类型（例如 `long long`，`double`））
  
- 初始化：`name.build(arr);`
  
  （其中 `arr` 表示初始的数组）
  
- 单点修改（单点加上一个数）：`name.modify1(k,x);`
  
  （其中 `k` 表示要修改的下标，`x` 表示要加上的数）
  
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
	class segtree1
	{
		private:
			struct node
			{
				int l;
				int r;
				T a;
				T lazy;
			} t[N << 2];
			inline int ls(int p) { return (p << 1); }
			inline int rs(int p) { return ((p << 1) | 1); }
			inline void push_up(int p) { t[p].a = t[ls(p)].a + t[rs(p)].a; }
			void push_down(int p)
			{
				t[ls(p)].lazy += t[p].lazy;
				t[rs(p)].lazy += t[p].lazy;
				t[ls(p)].a += (t[ls(p)].r - t[ls(p)].l + 1) * t[p].lazy;
				t[rs(p)].a += (t[rs(p)].r - t[rs(p)].l + 1) * t[p].lazy;
				t[p].lazy = 0;
			}
			void build_p(T arr[],int p,int l,int r)
			{
				t[p].l = l;
				t[p].r = r;
				if (l == r)
				{
					t[p].a = arr[l];
					return;
				}
				int mid = (l + r) >> 1;
				build_p(arr,ls(p),l,mid);
				build_p(arr,rs(p),mid + 1,r);
				push_up(p);
			}
			void modify1_p(int p,int k,T x)
			{
				if (t[p].l == t[p].r)
				{
					t[p].a += x;
					return;
				}
				int mid = (t[p].l + t[p].r) >> 1;
				if (k <= mid) modify1_p(ls(p),k,x);
				else modify1_p(rs(p),k,x);
				push_up(p);
			}
			T query1_p(int p,int k)
			{
				if (t[p].l == t[p].r) return t[p].a;
				push_down(p);
				int mid = (t[p].l + t[p].r) >> 1;
				if (k <= mid) return query1_p(ls(p),k);
				else return query1_p(rs(p),k);
			}
			void modify2_p(int p,int l,int r,T x)
			{
				if (l <= t[p].l && t[p].r <= r)
				{
					t[p].a += (t[p].r - t[p].l + 1) * x;
					t[p].lazy += x;
					return;
				}
				int mid = (t[p].l + t[p].r) >> 1;
				push_down(p);
				if (l <= mid) modify2_p(ls(p),l,r,x);
				if (r > mid) modify2_p(rs(p),l,r,x);
				push_up(p);
			}
			T query2_p(int p,int l,int r)
			{
				if (t[p].l > r || t[p].r < l) return 0;
				if (l <= t[p].l && t[p].r <= r) return t[p].a;
				push_down(p);
				return query2_p(ls(p),l,r) + query2_p(rs(p),l,r);
			}
		public:
			segtree1() { memset(t,0,sizeof t); }
			void build(T arr[]) { build_p(arr,1,1,N - 1); }
			void modify1(int k,T x) { modify1_p(1,k,x); }
			T query1(int k) { return query1_p(1,k); }
			void modify2(int l,int r,T x) { modify2_p(1,l,r,x); }
			T query2(int l,int r) { return query2_p(1,l,r); }
	};
}
```
## 压行版代码
```cpp
namespace tallnut{template<int N,typename T>class segtree1{private:struct node{int l;int r;T a;T lazy;}t[N<<2];inline int ls(int p){return(p<<1);}inline int rs(int p){return((p<<1)|1);}inline void push_up(int p){t[p].a=t[ls(p)].a+t[rs(p)].a;}void push_down(int p){t[ls(p)].lazy+=t[p].lazy;t[rs(p)].lazy+=t[p].lazy;t[ls(p)].a+=(t[ls(p)].r-t[ls(p)].l+1)*t[p].lazy;t[rs(p)].a+=(t[rs(p)].r-t[rs(p)].l+1)*t[p].lazy;t[p].lazy=0;}void build_p(T arr[],int p,int l,int r){t[p].l=l;t[p].r=r;if(l==r){t[p].a=arr[l];return;}int mid=(l+r)>>1;build_p(arr,ls(p),l,mid);build_p(arr,rs(p),mid+1,r);push_up(p);}void modify1_p(int p,int k,T x){if(t[p].l==t[p].r){t[p].a+=x;return;}int mid=(t[p].l+t[p].r)>>1;if(k<=mid)modify1_p(ls(p),k,x);else modify1_p(rs(p),k,x);push_up(p);}T query1_p(int p,int k){if(t[p].l==t[p].r)return t[p].a;push_down(p);int mid=(t[p].l+t[p].r)>>1;if(k<=mid)return query1_p(ls(p),k);else return query1_p(rs(p),k);}void modify2_p(int p,int l,int r,T x){if(l<=t[p].l&&t[p].r<=r){t[p].a+=(t[p].r-t[p].l+1)*x;t[p].lazy+=x;return;}int mid=(t[p].l+t[p].r)>>1;push_down(p);if(l<=mid)modify2_p(ls(p),l,r,x);if(r>mid)modify2_p(rs(p),l,r,x);push_up(p);}T query2_p(int p,int l,int r){if(t[p].l>r||t[p].r<l)return 0;if(l<=t[p].l&&t[p].r<=r)return t[p].a;push_down(p);return query2_p(ls(p),l,r)+query2_p(rs(p),l,r);}public:segtree1(){memset(t,0,sizeof t);}void build(T arr[]){build_p(arr,1,1,N-1);}void modify1(int k,T x){modify1_p(1,k,x);}T query1(int k){return query1_p(1,k);}void modify2(int l,int r,T x){modify2_p(1,l,r,x);}T query2(int l,int r){return query2_p(1,l,r);}};}
```
