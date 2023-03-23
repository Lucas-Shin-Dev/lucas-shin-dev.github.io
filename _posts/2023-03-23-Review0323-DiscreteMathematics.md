---
layout: single
title:  "Chapter 3. 집합론과 디지털적인 수의 세계"
categories: DiscreteMathematics
tag: [이산수학, 나작복]
toc: true
author_profile: false
sidebar:
    nav: "docs"
search: true #true, false
use_math: true
---

## 집합의 표현

원소(element)라 불리는 서로 다른 객체들의 모임.

어떤 객체가 그 집합에 속하는지 아닌지를 분명히 구분할 수 있어야 한다.(중복되는 원소 X)



집합을 표시할 땐느 알파벳 대문자로, 집합을 구성하는 원소는 알파벳 소문자로 나타낸다.

전체 집합(universal set): $U\$

공집합(empty set): $\empty\$, $\{ \}\$

정수 집합: $\Z\$

자연수의 집합: $N\$

실수의 집합: $R\$

유리수의 집합: $Q\$

1부터 n까지의 자연수의 집합: $S_n\$

유한 집합(finite set): 집합의 원소 개수가 유한한 집합

무한 집합(infinite set): 집합의 원소 개수가 무한한 집합



집합 A의 모든 원소가 집합 B의 원소에 속하면 '집합 A는 집합B에 포함된다.'라고 하고 A $\subseteq\$ B로 표기한다.

집합 A는 집합 B의 부분 집합(subset)이라 한다.

부분 집합이 아니면 A $\not\subset\$ B로 표기한다.

특히, A $\subseteq\$ B이고 A $\ne\$ B인 경우

집합 A를 집합 B의 진부분 집합(proper subset)이라 하고 A $\subset\$ B로 표기한다.

진부분 집합이 아니면 A $\not\subset\$ B로 표기한다.



집합 $U\$에 속하나 집합 A에 속하지 않는 원소들을 집합 A의 여집합(complement)라 하고  $\bar{A}\$ 또는 $A^\prime\$로 표기한다.



### 집합을 표현하는 방법

#### 원소 나열법

집합의 원소들을 { } 사이에 하나씩 나열

$S\$ = {1, 2, 3, 4, 5}



#### 조건 제시법

집합의 원소들이 가지고 있는 특저앟ㄴ 성질을 기술

$S\$ = {$x\$|$p(x)\$}

여기서 x는 변수이고 $p(x)\$는 원소들이 가지고 있는 성질이다.



#### 카디날리티(Cardinality)

집합 내에 있는 서로 다른 원소들의 개수

집합의 원소수라하고 |$S\$|로 표기한다.



#### 가산적 집합(countable set) & 가산적으로 무한한 집합(countably infinite set)

정수의 집합과 일대일 대응 관계에 있는 집합

ex) 자연수의 집합이 가산적으로 무한함을 보여라.

​	자연수의 집합과 정수 집합 사이에는 일대일 대응인 함수$f\$가 존재한다.

​	만약 $n\$이 홀수인 경우 $f(n)\$ = div($n\$, 2) +1인 함수가 적용되고 $n\$이 짝수인 경우에는 $f(n)\$ = -div($n\$, 2)의 식이 적용된다.

​	따라서 정수와 자연수는 일대일 대응 관계에 있으므로 자연수의 집합은 가산적이다.



## 집합의 연산

벤 다이어그램: 주어진 집합들 사이의 관계와 집합의 연산에 대해 쉽게 이해하기위해 이용된다.

​	(a) A $\subseteq\$ B

​	(b) 집합 A와 집합 B에 공통된 원소가 있을 때

​	(c) 집합 A와 집합 B에 공통된 원소가 없을 때

 ![image-20230323155046910]({{site.url}}\images\2023-03-23-Review0323-DiscreteMathematics\image-20230323155046910.png)

### 합집합 Union A $\cup B

집합 A 또는 집합 B에 속하는 모든 원소의 집합

A $\cup B = {$x\$ | $x\$ $\in\$ A $\or\$  $x\$ $\in\$ B}



### 교집합 Intersection A $\cap\$ B

집합 A와 집합 B에 속하는 모든 원소의 집합

A $\cap B = {$x\$ | $x\$ $\in\$ A $\and\$  $x\$ $\in\$ B}



### 서로소 Disjoint

집합 A와 집합 B가 공통된 원소를 하나도 가지지 않는 경우



### 차집합 Difference A - B

집합 A에 속하고 집합 B에 속하지 않은 모든 운소들의 집합

A - B = {$x\$| $x\$ $\in\$ A $\and\$ $x\$ $notin\$ B}



### 대칭 차집합 Synmetric Difference A $\oplus\$ B

A $\cup\$ B의 원소 중에서 A $\and\$ B에 속하지 않는 모든 원소들의 집합



### 곱집합 Cartesian Product A X B

순서쌍 (a, b)는 쌍의 원소들 간의 순서에 의해 구분이 된다.

a $\ne\$ b 이면 (a, b) $\ne\$ (b, a) 이고

(a, b) = (c, d) 이면 a = c 이고 b = d이다.



### 집합 연산의 카디날리티

집합의 원소의 개수는 |$S\$|로 표기한다.

​	a. |A $\cup\$ B| = |A| + |B| - |A $\cap\$ B|

​	b. |A $\cap\$ B| = |A| + |B| - |A $\cup\$ B| 

​	c. |A $\cup\$ B $\cup\$ C| = |A| + |B| + |C| - |A $\cap\$ B| - |B $\cap\$ C| - |A $\cap\$ C| + |A $\cap\$ B $\cap\$ C|

​	d. |A - B| = |A| - |A $\cap\$ B|

​	e. |A X B| = |A| $\cdot\$ |B|



### 집합의 대수 법칙

![image-20230323160824549]({{site.url}}\images\2023-03-23-Review0323-DiscreteMathematics\image-20230323160824549.png)

*집합에 관한 명제에서 그 명제 안에 있는 교집합과 합집합을 전체 집합에 대한 여집합으로 바꾸어서 만든 새로운 명제를 원래 명제의 쌍대(Duality)라고 한다.

쌍대의 원리를 이용하여 드 모르간 법칙 중 첫번째 식을 사용하면

(A$\cup\$B)^$\prime\$ = $A\$$\prime\$$\cap\$$B\$$\prime\$ $\leftrightarrow\$ (A$\cap\$B)^$\prime\$ = $A\$$\prime\$$\cup\$$B\$$\prime\$



## 집합류와 멱집합

집합류: 집합의 집합

​	집합 A에 대하여 A의 원소 개수가 n개일 때

​	집합 A의 부분 집합의 개수는 $2^n\$개

​	카다닐리티로 표현하면 $2^{|A|}\$개이다.



멱집합

​	임의의 집합 $S\$에 대하여 집합 $S\$의 모든 부분 집합을 원소로 가지는 집합을 집합 $S\$의 멱집합(power set)이라 한다.

​	$P(S)\$, $2^S\$로 표기한다.



멱집합의 주의점

	1. 멱집합을 구한 다음에는 멱집합의 원소의 개수가 $2^{|A|}\$개가 되는지 확인한다.
	1. 멱집합의 원소는 모두 지2ㅂ합이라는 점에 유의해야 한다.
	1. 원래 집합 A의 원소 중 집합인 원소가 있을 때에는 그 집합 자체가 하나의 원소이므로, 멱집합에서는 추가적인 집합 표기가 필요하다.



집합 A에 대하여 $P(A)\$의 원소들을 나타내기 위해 $A_1\$, $A_2\$, ... , $A_n\$으로 표기한다.

이들의 합집합을 $\underset{i=1}\overset{n}{\bigcup}\$$A_i\$, 교집합을 $\underset{i=1}\overset{n}{\bigcap}\$$A_i\$로 표기한다.



## 집합의 분할

분할의 원소인 $A_i\$를 분할의 블록(block)이라고 한다.

공집합이 아닌 임의의 집합 $S\$의 분할(partition) $\Pi\$는 다음 조건을 만족시켜야 한다.

	1. $i\$ = 1, ..., $k\$에 대하여 $A_i\$는 공집합이 아닌 집합 $S\$의 부분 집합이다.
	1. $S\$ = $A_1\$$\cup\$$A_2\$$\cup\$...$\cup\$$A_n\$
	1. $A_i\$들 사이에서는 서로소이다. 즉, $i\$$\ne\$$j\$이면, $A_i\$$\cap\$$A_j\$ = $\0\$이다.

![image-20230323200335965]({{site.url}}\images\2023-03-23-Review0323-DiscreteMathematics\image-20230323200335965.png)



## 수의 표현과 진법의 변환

[Digital Design Number-Base Conversion](https://lucas-shin-dev.github.io/digitaldesign/Review0315-DigitalDesign0315/#number-base-conversions)

다음 주소로 들어가면 진법 변환에 대해 자세히 확인할 수 있습니다.



## 2진수의 덧셈과 뺄셈

[Digital Design Subtraction](https://lucas-shin-dev.github.io/digitaldesign/Review0315-DigitalDesign0315/#subtraction-with-complement)

다음 주소로 들어가면 2진수의 덧셈과 뺄셈에 대해 자세히 확인할 수 있습니다.
