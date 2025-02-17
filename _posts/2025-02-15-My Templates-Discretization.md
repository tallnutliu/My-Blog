# 蒟蒻 tallnut 的模板库 - 离散化

## [返回模板库目录](https://tallnutliu.github.io/2025/02/15/My-Templates-(Chinese-version).html)

## 功能
实现了一个对数组进行离散化的函数。

## 使用方式
`discretize(arr,n);`

（其中 `arr` 表示数组名，`n` 表示长度）

## 代码所需头文件
```cpp
#include <algorithm>
```

## 代码
```cpp
namespace tallnut
{
	template <typename T>
	void discretize(T a[],int n)
	{
		T b[n + 1];
		for (int i = 1;i <= n;i++)
			b[i] = a[i];
		std::sort(b + 1,b + n + 1);
		int len = std::unique(b + 1,b + n + 1) - b - 1;
		for (int i = 1;i <= n;i++)
			a[i] = std::lower_bound(b + 1,b + len + 1,a[i]) - b;
	}
}
```

## 压行版代码
```cpp
namespace tallnut{template<typename T>void discretize(T a[],int n){T b[n+1];for(int i=1;i<=n;i++)b[i]=a[i];std::sort(b+1,b+n+1);int len=std::unique(b+1,b+n+1)-b-1;for(int i=1;i<=n;i++)a[i]=std::lower_bound(b+1,b+len+1,a[i])-b;}}
```
