---
layout: post
title:  "“最大公约数” 和 “最小公倍数”"
date:   2018-03-17 23:08:00 +0800
categories: 算法
tags: 算法
---

## 最大公约数 Greatest Common Divisor(GCD)
#### 辗转相除法求最大公约数(欧几里得算法)

```java
//求a和b的最大公约数
int gcd(int a, int b){
	return b==0?a:gcd(b,a%b);	
}
```

## 最小公倍数 Least Common Multiple(LCM)

```java
//常识： a和b的最小公倍数=a*b/(a和b的最大公约数)
int lcm(int a, int b){
	return a*b/gcd(a,b);
}
```
