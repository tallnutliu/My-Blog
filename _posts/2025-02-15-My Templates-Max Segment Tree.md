# 蒟蒻 tallnut 的模板库 - max 线段树
## [返回模板库目录](https://www.luogu.com.cn/paste/yw5teupm)
## 功能
这个类实现了单点修改最大值、单点或区间查询最大值线段树功能。
## 使用方式
- 定义：`segtree2<N,T> name;`
  
  （其中 `N` 表示线段树要存储的元素个数，`T` 表示线段树存储的类型（例如 `long long`，`double`））
  
- 初始化：`name.build(arr);`
  
  （其中 `arr` 表示初始的数组）
  
- 单点修改（单点更新为最大值）：`name.modify(k,x);`
  
  （其中 `k` 表示要修改的下标，`x` 表示要更新的数）
  
- 单点查询（获取单点的值）：`name.query1(k)`
  
  （其中 `k` 表示要查询的下标）

- 区间查询（获取区间的最大值）：`name.query2(l,r)`
  
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
    class segtree2
    {
        private:
            struct node
            {
                int l;
                int r;
                T a;
            } t[N << 2];
            inline int ls(int p) { return (p << 1); }
            inline int rs(int p) { return ((p << 1) | 1); }
            inline void push_up(int p) { t[p].a = std::max(t[ls(p)].a,t[rs(p)].a); }
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
            void modify_p(int p,int k,T x)
            {
                if (t[p].l == t[p].r)
				{
					t[p].a = std::max(t[p].a,x);
					return;
				}
				int mid = (t[p].l + t[p].r) >> 1;
				if (k <= mid) modify_p(ls(p),k,x);
				else modify_p(rs(p),k,x);
				push_up(p);
            }
            T query1_p(int p,int k)
			{
				if (t[p].l == t[p].r) return t[p].a;
				int mid = (t[p].l + t[p].r) >> 1;
				if (k <= mid) return query1_p(ls(p),k);
				else return query1_p(rs(p),k);
			}
            T query2_p(int p,int l,int r)
            {
                if (t[p].l > r || t[p].r < l) return 0;
				if (l <= t[p].l && t[p].r <= r) return t[p].a;
				return std::max(query2_p(ls(p),l,r),query2_p(rs(p),l,r));
            }
        public:
            segtree2() { memset(t,0,sizeof t); }
			void build(T arr[]) { build_p(arr,1,1,N - 1); }
			void modify(int k,T x) { modify_p(1,k,x); }
			T query1(int k) { return query1_p(1,k); }
			T query2(int l,int r) { return query2_p(1,l,r); }
    };
}
```
## 压行版代码
```cpp
namespace tallnut{template<int N,typename T>class segtree2{private:struct node{int l;int r;T a;}t[N<<2];inline int ls(int p){return(p<<1);}inline int rs(int p){return((p<<1)|1);}inline void push_up(int p){t[p].a=std::max(t[ls(p)].a,t[rs(p)].a);}void build_p(T arr[],int p,int l,int r){t[p].l=l;t[p].r=r;if(l==r){t[p].a=arr[l];return;}int mid=(l+r)>>1;build_p(arr,ls(p),l,mid);build_p(arr,rs(p),mid+1,r);push_up(p);}void modify_p(int p,int k,T x){if(t[p].l==t[p].r){t[p].a=std::max(t[p].a,x);return;}int mid=(t[p].l+t[p].r)>>1;if(k<=mid)modify_p(ls(p),k,x);else modify_p(rs(p),k,x);push_up(p);}T query1_p(int p,int k){if(t[p].l==t[p].r)return t[p].a;int mid=(t[p].l+t[p].r)>>1;if(k<=mid)return query1_p(ls(p),k);else return query1_p(rs(p),k);}T query2_p(int p,int l,int r){if(t[p].l>r||t[p].r<l)return 0;if(l<=t[p].l&&t[p].r<=r)return t[p].a;return std::max(query2_p(ls(p),l,r),query2_p(rs(p),l,r));}public:segtree2(){memset(t,0,sizeof t);}void build(T arr[]){build_p(arr,1,1,N-1);}void modify(int k,T x){modify_p(1,k,x);}T query1(int k){return query1_p(1,k);}T query2(int l,int r){return query2_p(1,l,r);}};}
```
