# 蒟蒻 tallnut 的模板库 - 并查集

## [返回模板库目录](https://tallnutliu.github.io/My-Blog/2025/02/15/My-Templates-(Chinese-version).html)

## 功能
这个类实现了合并和查询集合的并查集功能。

## 使用方式
- 定义：`dsu<N> name;`
  
  （其中 `N` 表示并查集要存储的元素个数）
  
- 合并两个元素所处的集合：`name.merge(x,y);`
  
  （其中 `x,y` 表示两个元素）
  
- 查询两个元素是否处于同一集合：`name.query(x,y)`
  
  （其中 `x,y` 表示两个元素）

## 代码所需头文件
无。

## 代码
```cpp
namespace tallnut
{
    template <int N>
    class dsu
    {
        private:
            int fa[N];
            int siz[N];
      		int find(int x)
            {
                if (fa[x] == x) return x;
                return fa[x] = find(fa[x]);
            }
        public:
            dsu()
            {
                for (int i = 1;i < N;i++)
                    fa[i] = i;
            }
            void merge(int x,int y)
            {
                int fax = find(x);
                int fay = find(y);
                if (fax == fay) return;
                if (siz[fax] > siz[fay]) swap(fax,fay);
                siz[fay] += siz[fax];
                fa[fax] = fay;
            }
            bool query(int x,int y) { return find(x) == find(y); }
    };
}
```

## 压行版代码
```cpp
namespace tallnut{template<int N>class dsu{private:int fa[N];int siz[N];int find(int x){if(fa[x]==x)return x;return fa[x]=find(fa[x]);}public:dsu(){for(int i=1;i<N;i++)fa[i]=i;}void merge(int x,int y){int fax=find(x);int fay=find(y);if(fax==fay)return;if(siz[fax]>siz[fay])swap(fax,fay);siz[fay]+=siz[fax];fa[fax]=fay;}bool query(int x,int y){return find(x)==find(y);}};}
```
