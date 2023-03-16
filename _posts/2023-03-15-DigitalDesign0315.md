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

$a_5*a_4*a_3*a_2*a_1*a_0*a_-1*a_-2*a_-3\$

$ = a_5*r^5+a_4*r^4+a_3*r^3+a_2*r^2+a_1*r^1+a_0*r^0+a_-1*r^-1+a_-2*r^-2+a_-3*r^2-3\$

산술 연산은 decimal(10진법)과 같은 규칙으로 연산한다.



## Number-base conversions

decimal -> r로 변환하려면 숫자와 모든 연속적인 몫을 r로 나누고 나머지를 모으면 된다.

decimal의 소수는 나누는 대신 1만 남을 때까지 곱한다. 



### 2 number system

2진수는 10진수로 나타낸 수에 2로 나누거나 곱하여 구할 수 있다.

![image-20230315163339722](C:\Users\wymam\AppData\Roaming\Typora\typora-user-images\image-20230315163339722.png)

![image-20230315163359898](C:\Users\wymam\AppData\Roaming\Typora\typora-user-images\image-20230315163359898.png)

따라서 $(41.06875)_(10)$는 2진수로 변환하면 $(101001.1011)_2$로 나타낼 수 있다.



### 8 number system & 16 number system

8진수는 10진수로 나타낸 수에 8로 나누거나 곱하여 구할 수 있다.

그러나 8로 나누거나 곱하기 어렵기 때문에 10진수를 2진수로 변환한 다음 2진수의 소수점을 기준으로 세자리씩 묶어 8진수로 변환하면 보다 쉽게 10진수에서 8진수로 변환할 수 있다.



마찬가지로 16진수도 16으로 나누거나 곱하여 구할 수 있으나 불편하기 때문에 10진수를 2진수로 변환한 다음 2진수의 소수점을 기준으로 네자리씩 묶어 16진수로 변환하면 보다 쉽게 10진수에서 16진수로 변환할 수 있다.

### Complement(보수)

수의 보수에는 2가지 방법이 있다.

 1. Diminished Radix Complement(감소된 기수 보수)

 2. Radix Complement(기수 보수)

    

### Diminished Radix Complement

N의 (r-1)'s complement로 식으로 나타내면 $(r^n-1)-N\$이다.

Decimal number에서는 9's complement로 9에서 각 자리 숫자를 뺀 값으로 나타난다.

ex) 546700의 9's complement는 453299이다.

Binary number에서는 1's complement로 1에서 각 자리 숫자를 뺸 값으로 나타난다.

결과적으로 0은 1로, 1은 0으로 바꾼 값과 동일하다.

ex) 1011000읜 1's complement는 0100111이다.



### Radix Complement

N의 r's complement로 식으로 나타내면 $r^n-N\$이다.

정의상 Radix Complement는 Diminished Radix Complement에 1을 더한 값이다.

$r^n-N = ((r^n-1)-N)+1\$

즉 (r-1)'s complement를 구한 뒤 1을 더해준다.

Decimal number에서는 10's complement로 9에서 각 자리 숫자를 뺴되 0이 아닌 최하위 유효 자릿수는 10에서 뺀다.

ex) 012398의 10's complement는 987602이다.

Binary number에서는 2's complement로 1에서 각 자리 숫자를 뺸 뒤 1을 더해준 값으로 나타난다.

결과적으로 모든 최하위 유효 자리 0과 첫번째 1은 그대로 두고 나머지 모든 상위 유효 자리는 0을 1로, 1을 0으로 바꾼 값과 동일하다.



## Subtraction with Complement

### r's Complement를 이용하는 방법(주로 이용)

$M + (r^n-N) = (M - N) + r^n\$ (피감수 M, 감수 N)

 1. $M >= N\$이면 결과는 M - N, end carry $r^n\$은 버린다.

 2. $M<N\$이면 결과는 $r^n-(N-M) 즉 (N-M)의 r's complement를 취한 뒤 (-)를 붙인다.

     

### (r-1)'s Complement를 이용하는 방법

$M + ((r^n-1)-N) = (M - N) + (r^n-1)\$ (피감수 M, 감수 N)

 1. $M >= N\$이면 결과는 M - N, end carry $r^n\$은 버린 후 1을 더해준다.(이를 end around carry라고 한다.)

 2. $M<N\$이면 결과는 $(r^n-1)-(N-M) 즉 (N-M)의 (r-1)'s complement를 취한 뒤 (-)를 붙인다.

    



## Signed Binary Number

unsigned binary number는 4bit system에서 0부터 15까지 표현이 가능하다.

그러나 음수는 어떻게 표현해야할까?

우선 최상위 비트롤 부호 비트로 할당하여 0일경우 양수를 1일 경우 음수를 나타낸다.

구체적으로 음수를 나타내기 위해 3가지 방법이 있다.

 1. Signed Magnitude Representation

 2. Signed 1's Complement Representation

 3. Signed 2's Complement Representation

    

3가지 방법은 4bit system을 가정하고 설명하겠다.

### Signed Magnitude Representation

양수와 음수의 크기 비트는 동일하고 부호 비트만 0과 1로 양수와 음수를 나타낸다.

ex) 

0101 -> 5

1101 -> -5

이 표현법의 단점은 0의 중복이다.(0000과 1000은 +0과 -0으로 동일하다.)

또한 일반적인 산술 연산을 할 경우 부호 비트와 크기 비트를 나눠야해서 불편하다.

