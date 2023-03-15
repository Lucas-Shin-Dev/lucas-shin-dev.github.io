---
layout: single
title:  "Chapter 1. 디지털 시스템과 2진수"
categories: DigitalDesign
tag: [디지털디자인, 나작복]
toc: true
author_profile: false
sidebar:
    nav: "docs"
search: true #true, false
use_math: true
---

## r number system

r은 base numer(기수)이다.

r number system의 예로

10 number system, r=10, decimal 10진법

2 number system, r=2, binary 2진법

8 number system, r=8, octal 8진법

16 number system, r=16, hexadecimal 16진법이 있다

$a_5*a_4*a_3*a_2*a_1*a_0*a_-1*a_-2*a_-3$

$ = a_5*r^5+a_4*r^4+a_3*r^3+a_2*r^2+a_1*r^1+a_0*r^0+a_-1*r^-1+a_-2*r^-2+a_-3*r^2-3$

산술 연산은 decimal(10진법)과 같은 규칙으로 연산한다.



## Number-base conversions

decimal -> r로 변환하려면 숫자와 모든 연속적인 몫을 r로 나누고 나머지를 모으면 된다.

decimal의 소수는 나누는 대신 1만 남을 때까지 곱한다. 



### 2 number system

2진수는 10진수로 나타낸 수에 2로 나누거나 곱하여 구할 수 있다.

![image-20230315163339722](C:\Users\wymam\AppData\Roaming\Typora\typora-user-images\image-20230315163339722.png)

![image-20230315163359898](C:\Users\wymam\AppData\Roaming\Typora\typora-user-images\image-20230315163359898.png)

따라서 $(41.06875)_10$는 2진수로 변환하면 $(101001.1011)_2$로 나타낼 수 있다.



### 8 number system & 16 number system

8진수는 10진수로 나타낸 수에 8로 나누거나 곱하여 구할 수 있다.

그러나 8로 나누거나 곱하기 어렵기 때문에 10진수를 2진수로 변환한 다음 2진수의 소수점을 기준으로 세자리씩 묶어 8진수로 변환하면 보다 쉽게 10진수에서 8진수로 변환할 수 있다.



마찬가지로 16진수도 16으로 나누거나 곱하여 구할 수 있으나 불편하기 때문에 10진수를 2진수로 변환한 다음 2진수의 소수점을 기준으로 네자리씩 묶어 16진수로 변환하면 보다 쉽게 10진수에서 16진수로 변환할 수 있다.

