---
title: Something about \_\_gcd
urlname: sp-gcd
categories: Algorithm
tags: 
- "Algorithm"
- "c/c++"
image: https://i.loli.net/2019/07/18/5d301d32b2f0631960.jpg
---
I have written an article about gcd and lcm,I meet a new way to calculate gcd these days.<!-- more-->
For example: 
```
#include<algorithm>
#include<cstdio>
using namespace std;
int main()
{
	int a=199,b=199*2;
	printf("%d\n",__gcd(a,b));
}

output: 
199
```
The header file of \_\_gcd is 'algorithm'.
How about the Time complexity(时间复杂度) of it.
I found the source code for its implementation in the source file.Just like Division algorithm(辗转相除法).
```
  /**
   *  This is a helper function for the rotate algorithm specialized on RAIs.
   *  It returns the greatest common divisor of two integer values.
  */
  template<typename _EuclideanRingElement>
    _EuclideanRingElement
    __gcd(_EuclideanRingElement __m, _EuclideanRingElement __n)
    {
      while (__n != 0)
	{
	  _EuclideanRingElement __t = __m % __n;
	  __m = __n;
	  __n = __t;
	}
      return __m;
    }
```
Now it's clear that the Time complexity(时间复杂度) of it is log(n).
About this function,many people say it's probably forbidden in some test,and gcd is not so hard to write,just get too know it.