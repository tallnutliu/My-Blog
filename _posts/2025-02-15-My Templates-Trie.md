# 蒟蒻 tallnut 的模板库 - 字典树

## [返回模板库目录](https://tallnutliu.github.io/2025/02/15/My-Templates-(Chinese-version).html)

## 功能
这个类实现了前缀个数查询字典树功能。

## 使用方式
- 定义：`trie<N> name;`
  
  （其中 `N` 表示字符串长度之和的最大值）
  
- 插入一个模式串：`name.insert(s);`
  
  （其中 `s` 表示要插入的 `std::string`）
  
- 查询：`name.query(s)`
  
  （其中 `s` 表示要查询的 `std::string`）

## 代码所需头文件
```cpp
#include <cstring>
#include <cctype>
```

## 代码
```cpp
namespace tallnut
{
    int trieidx = 0;
    template <int N>
    class trie
    {
        private:
            int child[N][63],cnt[N];
            int get(char c)
            {
                if (islower(c))
                    return c - 'a';
                else if (isupper(c))
                    return c - 'A' + 26;
                else
                    return c - '0' + 52;
            }
        public:
            trie()
            {
                for (int i = 0;i <= trieidx;i++)
                    memset(child[i],0,sizeof child[i]);
                for (int i = 0;i <= trieidx;i++)
                    cnt[i] = 0;
                trieidx = 0;
            }
            void insert(const std::string& s)
            {
                int cur = 0;
                for (int i = 0;i < s.size();i++)
                {
                    int c = get(s[i]);
                    if (!child[cur][c])
                        child[cur][c] = ++trieidx;
                    cur = child[cur][c];
                    cnt[cur]++;
                }
            }
            int query(const std::string& s)
            {
                int cur = 0;
                for (int i = 0;i < s.size();i++)
                {
                    int c = get(s[i]);
                    if (!child[cur][c])
                        return 0;
                    cur = child[cur][c];
                }
                return cnt[cur];
            }
    };
}
```

## 压行版代码
```cpp
namespace tallnut{int trieidx=0;template<int N>class trie{private:int child[N][63],cnt[N];int get(char c){if(islower(c))return c-'a';else if(isupper(c))return c-'A'+26;else return c-'0'+52;}public:trie(){for(int i=0;i<=trieidx;i++)memset(child[i],0,sizeof child[i]);for(int i=0;i<=trieidx;i++)cnt[i]=0;trieidx=0;}void insert(const std::string&s){int cur=0;for(int i=0;i<s.size();i++){int c=get(s[i]);if(!child[cur][c])child[cur][c]=++trieidx;cur=child[cur][c];cnt[cur]++;}}int query(const std::string&s){int cur=0;for(int i=0;i<s.size();i++){int c=get(s[i]);if(!child[cur][c])return 0;cur=child[cur][c];}return cnt[cur];}};}
```
