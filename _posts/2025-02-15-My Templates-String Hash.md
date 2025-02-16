# 蒟蒻 tallnut 的模板库 - 字符串哈希

## [返回模板库目录](https://tallnutliu.github.io/My-Blog/2025/02/15/My-Templates-(Chinese-version).html)

## 功能
这个类实现了查询给定字符串的子串哈希值的功能，底层使用了双哈希。

## 使用方式
- 定义：`stringhash name;`

- 初始化：`name.init(s,bas1,md1,bas2,md2);`
  
  （其中 `s` 表示原始字符串（序号从 `0` 开始，即不需要在开头插入占位符），`bas1` 表示第一组哈希的基底，`md1` 表示第一组哈希的模数，`bas2` 表示第二组哈希的基底，`md2` 表示第二组哈希的模数，`bas1,md1,bas2,md2` 可省略，若省略则使用默认参数）
  
- 查询：`name.query(l,r)`
  
  （其中 `l,r` 表示该区间的左端点和右端点，**注意，返回值为 `unsigned long long` 类型，为两组哈希打包在一起的值**）

## 代码所需头文件
```cpp
#include <cctype>
```

## 代码
```cpp
namespace tallnut
{
	class stringhash
	{
		private:
			unsigned base1,mod1,base2,mod2;
			unsigned long long *a1,*pw1,*a2,*pw2;
			bool used;
			int get(char c)
			{
				if (islower(c))
                    return c - 'a';
                else if (isupper(c))
                    return c - 'A' + 26;
                else
                    return c - '0' + 52;
			}
			unsigned long long q1(int l,int r) { return ((a1[r] - (a1[l - 1] * pw1[r - l + 1] % mod1) + mod1) % mod1); }
			unsigned long long q2(int l,int r) { return ((a2[r] - (a2[l - 1] * pw2[r - l + 1] % mod2) + mod2) % mod2); }
		public:
			stringhash() { used = false; }
			void init(const string& s,unsigned bas1 = 101,unsigned md1 = 998244353,unsigned bas2 = 131,unsigned md2 = 1e9 + 7)
			{
				if (used)
				{
					delete[] a1;
					delete[] pw1;
					delete[] a2;
					delete[] pw2;
				}
				base1 = bas1;
				mod1 = md1;
				base2 = bas2;
				mod2 = md2;
				used = true;
				int len = s.size();
				a1 = new unsigned long long[len + 1];
				a1[0] = 0;
				for (int i = 0;i < len;i++)
					a1[i + 1] = (a1[i] * base1 + get(s[i])) % mod1;
				pw1 = new unsigned long long[len + 1];
				pw1[0] = 1;
				for (int i = 1;i <= len;i++)
					pw1[i] = pw1[i - 1] * base1 % mod1;
				a2 = new unsigned long long[len + 1];
				a2[0] = 0;
				for (int i = 0;i < len;i++)
					a2[i + 1] = (a2[i] * base2 + get(s[i])) % mod2;
				pw2 = new unsigned long long[len + 1];
				pw2[0] = 1;
				for (int i = 1;i <= len;i++)
					pw2[i] = pw2[i - 1] * base2 % mod2;
			}
			unsigned long long query(int l,int r) { return (q1(l,r) << 32) + q2(l,r);	}
			~stringhash()
			{
				if (used)
				{
					delete[] a1;
					delete[] pw1;
					delete[] a2;
					delete[] pw2;
				}
			}
	};
}
```

## 压行版代码
```cpp
namespace tallnut{class stringhash{private:unsigned base1,mod1,base2,mod2;unsigned long long*a1,*pw1,*a2,*pw2;bool used;int get(char c){if(islower(c))return c-'a';else if(isupper(c))return c-'A'+26;else return c-'0'+52;}unsigned long long q1(int l,int r){return((a1[r]-(a1[l-1]*pw1[r-l+1]%mod1)+mod1)%mod1);}unsigned long long q2(int l,int r){return((a2[r]-(a2[l-1]*pw2[r-l+1]%mod2)+mod2)%mod2);}public:stringhash(){used=false;}void init(const string&s,unsigned bas1=101,unsigned md1=998244353,unsigned bas2=131,unsigned md2=1e9+7){if(used){delete[]a1;delete[]pw1;delete[]a2;delete[]pw2;}base1=bas1;mod1=md1;base2=bas2;mod2=md2;used=true;int len=s.size();a1=new unsigned long long[len+1];a1[0]=0;for(int i=0;i<len;i++)a1[i+1]=(a1[i]*base1+get(s[i]))%mod1;pw1=new unsigned long long[len+1];pw1[0]=1;for(int i=1;i<=len;i++)pw1[i]=pw1[i-1]*base1%mod1;a2=new unsigned long long[len+1];a2[0]=0;for(int i=0;i<len;i++)a2[i+1]=(a2[i]*base2+get(s[i]))%mod2;pw2=new unsigned long long[len+1];pw2[0]=1;for(int i=1;i<=len;i++)pw2[i]=pw2[i-1]*base2%mod2;}unsigned long long query(int l,int r){return(q1(l,r)<<32)+q2(l,r);}~stringhash(){if(used){delete[]a1;delete[]pw1;delete[]a2;delete[]pw2;}}};}
```
