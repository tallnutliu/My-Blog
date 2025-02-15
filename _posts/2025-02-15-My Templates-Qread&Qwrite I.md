# 蒟蒻 tallnut 的模板库 - 快读、快写
## [返回模板库目录](https://www.luogu.com.cn/paste/yw5teupm)
## 功能
这实现了一些函数，支持对 `int`，`unsigned`，`long long`，`unsigned long long` 的快读、快写。
## 使用方式
- 快读：`qread(n);`
  
  （其中 `n` 为要读入的整数名称）
  
- 快写：`qwrite(n);`
  
  （其中 `n` 为要输出的整数名称）
## 代码所需头文件
```cpp
#include <cstdio>
#include <cctype>
```
## 代码
```cpp
namespace tallnut
{
	void qread(int& x)
	{
		char c = getchar();
		bool flag = false;
		while ((!isdigit(c)) && (c != '-'))
			c = getchar();
		if (c == '-')
		{
			flag = true;
			c = getchar();
		}
		x = 0;
		while (isdigit(c))
		{
			x = (x << 3) + (x << 1) + c - '0';
			c = getchar();
		}
		if (flag) x = -x;
	}
	void qread(unsigned& x)
	{
		char c = getchar();
		while (!isdigit(c))
			c = getchar();
		x = 0;
		while (isdigit(c))
		{
			x = (x << 3) + (x << 1) + c - '0';
			c = getchar();
		}
	}
	void qread(long long& x)
	{
		char c = getchar();
		bool flag = false;
		while ((!isdigit(c)) && (c != '-'))
			c = getchar();
		if (c == '-')
		{
			flag = true;
			c = getchar();
		}
		x = 0;
		while (isdigit(c))
		{
			x = (x << 3) + (x << 1) + c - '0';
			c = getchar();
		}
		if (flag) x = -x;
	}
	void qread(unsigned long long& x)
	{
		char c = getchar();
		while (!isdigit(c))
			c = getchar();
		x = 0;
		while (isdigit(c))
		{
			x = (x << 3) + (x << 1) + c - '0';
			c = getchar();
		}
	}
	void qwrite(int x)
	{
		if (x == 0)
		{
			putchar('0');
			return;
		}
		if (x < 0)
		{
			putchar('-');
			x = -x;
		}
		int stack[11];
		int cnt = 0;
		while (x)
		{
			stack[++cnt] = x % 10;
			x /= 10;
		}
		while (cnt)
			putchar(stack[cnt--] + '0');
	}
	void qwrite(unsigned x)
	{
		if (x == 0)
		{
			putchar('0');
			return;
		}
		int stack[11];
		int cnt = 0;
		while (x)
		{
			stack[++cnt] = x % 10;
			x /= 10;
		}
		while (cnt)
			putchar(stack[cnt--] + '0');
	}
	void qwrite(long long x)
	{
		if (x == 0)
		{
			putchar('0');
			return;
		}
		if (x < 0)
		{
			putchar('-');
			x = -x;
		}
		int stack[20];
		int cnt = 0;
		while (x)
		{
			stack[++cnt] = x % 10;
			x /= 10;
		}
		while (cnt)
			putchar(stack[cnt--] + '0');
	}
	void qwrite(unsigned long long x)
	{
		if (x == 0)
		{
			putchar('0');
			return;
		}
		int stack[20];
		int cnt = 0;
		while (x)
		{
			stack[++cnt] = x % 10;
			x /= 10;
		}
		while (cnt)
			putchar(stack[cnt--] + '0');
	}
}
```
## 压行版代码
```cpp
namespace tallnut{void qread(int&x){char c=getchar();bool flag=false;while((!isdigit(c))&&(c!='-'))c=getchar();if(c=='-'){flag=true;c=getchar();}x=0;while(isdigit(c)){x=(x<<3)+(x<<1)+c-'0';c=getchar();}if(flag)x=-x;}void qread(unsigned&x){char c=getchar();while(!isdigit(c))c=getchar();x=0;while(isdigit(c)){x=(x<<3)+(x<<1)+c-'0';c=getchar();}}void qread(long long&x){char c=getchar();bool flag=false;while((!isdigit(c))&&(c!='-'))c=getchar();if(c=='-'){flag=true;c=getchar();}x=0;while(isdigit(c)){x=(x<<3)+(x<<1)+c-'0';c=getchar();}if(flag)x=-x;}void qread(unsigned long long&x){char c=getchar();while(!isdigit(c))c=getchar();x=0;while(isdigit(c)){x=(x<<3)+(x<<1)+c-'0';c=getchar();}}void qwrite(int x){if(x==0){putchar('0');return;}if(x<0){putchar('-');x=-x;}int stack[11];int cnt=0;while(x){stack[++cnt]=x%10;x/=10;}while(cnt)putchar(stack[cnt--]+'0');}void qwrite(unsigned x){if(x==0){putchar('0');return;}int stack[11];int cnt=0;while(x){stack[++cnt]=x%10;x/=10;}while(cnt)putchar(stack[cnt--]+'0');}void qwrite(long long x){if(x==0){putchar('0');return;}if(x<0){putchar('-');x=-x;}int stack[20];int cnt=0;while(x){stack[++cnt]=x%10;x/=10;}while(cnt)putchar(stack[cnt--]+'0');}void qwrite(unsigned long long x){if(x==0){putchar('0');return;}int stack[20];int cnt=0;while(x){stack[++cnt]=x%10;x/=10;}while(cnt)putchar(stack[cnt--]+'0');}}
```
