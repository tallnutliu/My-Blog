# 蒟蒻 tallnut 的模板库 - 缺省源

## [返回模板库目录](https://tallnutliu.github.io/My-Blog/2025/02/15/My-Templates-(Chinese-version).html)

## 功能
一个缺省源，没什么好说的。（适用于 VS Code）

## 使用方式
注释里面有。

## 代码
```cpp
// NOTE: "[EDIT]" means you should edit this part by yourself
#include <bits/stdc++.h>
// [EDIT] please enable this line if there are many tests
//#define MULTITEST
using namespace std;
// [EDIT] if you want to copy some templates, please paste them here

typedef long long ll;
#define rep1(i,x,y) for (int i = (x);i <= (y);i++)
#define rep2(i,x,y) for (int i = (x);i >= (y);i--)
#define rep3(i,x,y,z) for (int i = (x);i <= (y);i += (z))
#define rep4(i,x,y,z) for (int i = (x);i >= (y);i -= (z))
#define cl(a) memset(a,0,sizeof(a))
// [EDIT] define some constants here

// [EDIT] define some variables, arrays, etc here

// [EDIT] a function to solve the problem
void solve()
{
    //input
    
    //solve
    
    //output
    
    //clear
    
}
int main()
{
#ifdef ONLINE_JUDGE
    ios::sync_with_stdio(false);
    cin.tie(0);
    cout.tie(0);
#endif
    int t;
#ifdef MULTITEST
    cin >> t;
#else
    t = 1;
#endif
    while (t--)
        solve();
#ifndef ONLINE_JUDGE
    cout << "\n---------------\n";
    system("pause");
#endif
}
```
