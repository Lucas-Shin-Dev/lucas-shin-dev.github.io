---
layout: single
title:  "Chapter 5. 관계"
categories: DiscreteMathematics
tag: [이산수학, 나작복]
toc: true
author_profile: false
sidebar:
    nav: "docs"
search: true #true, false
use_math: true
---



## 관계와 이항 관계

* 관계는 집합에서의 원소들 간의 순서(order)를 고려한 것이다.

* 원소들 간에 '$<\$', '$\le\$', '$\equiv\$', '$\subset\$' ... 등의 관계 연산자를 사용한다.

* 관계의 집합에 대한 연산, 즉 교집합, 합집합, 여집합, 차집합 등도 관계를 가진다.

* 두 개의 숫자 x, y에 대해서도 x < y 이거나, x가 y를 나눌 수 있을 때 등 여러 경우에 대해 서로 관계가 있다.



> 두 집합 A, B에 대하여, A로부터 B로의 이항 관계(binary relation) R은 두 집합의 곱집합 A X B의 부분 집합이다.
>
> A X B의 원소인 순서쌍 (a, b)가 주어졌을 때 (a, b) $\in\$ R과 aRb는 동치이다.



aRb $\Leftrightarrow\$ (a, b) $\in\$ R : a와 b가 관계가 있는 경우

a$\cancel{R}\$b $\nLeftrightarrow\$ (a, b) $\notin\$ R : a와 b가 관계가 없는 경우



첫번째 원소의 집합을 정의역(domain)이라 하고 Dom(R)로 표시한다.

두번째 원소의 집합을 치역(range)이라 하고 Ran(R)로 표시한다.



> 집합 A에서 집합 B로의 관계 R에 대한 역관계(inverse relation) $R^{-1}\$는 집합 B에서 집합 A로의 관계를 나타낸다.
>
> $R^{-1}\$ = {(b, a) $\mid\$ (a, b) $\in\$ R}
>
> 즉, aRb의 관계가 있어야만 b$R^{-1}\$a가 존재하게 된다.



## 관계의 표현

* 서술식 방법 : '집합 A = {1, 2, 3}에 서 원소 a, b가 a  $\ge\$ b인 관계 R'과 같이 직접 서술
* 나열식 방법: 서술식에 따라 관계를 순서쌍들의 집합으로 표현



### 화살표 도표 (Arrow Diagram)

a가 집합 A의 원소이고, b가 집합 B의 원소라 가정할 때 (a, b) $\in\$ R일 경우 집합 A에 있는 원소 a에서 집합 B에 있는 원소 b로 화살표를 그려서 표현한다.

![image-20230406094634977]({{site.url}}\images\2023-04-06-Review0406-DiscreteMathematics\image-20230406094634977.png)



### 좌표 도표 (Coordinate Diagram)

집합 A의 원소를 x축 위의 점으로 표시하고 집합 B의 원소를 y축 위의 점으로 생각한다.

a $\in\$ A 와 b $\in\$ B가 관계가 있으면 a를 가리키는 x 좌표축과 b를 가리키는 y 좌표축이 만나는 곳에 점으로 표시한다.

![image-20230406094844868]({{site.url}}\images\2023-04-06-Review0406-DiscreteMathematics\image-20230406094844868.png)



### 방향 그래프 (Directed Graph)

관계 R이 두 집합 A와 B 사이의 관계가 아니고 하나의 집합 A에 대한 관계라고 할 때

집합 A의 각 원소를 그래프의 정점(vertex)으로 표시한다.

(a, b) $\in\$ R일 경우 a에서 b로의 화살표가 있는 연결선(edge)인 방향 그래프로 표현한다.

![image-20230406095019029]({{site.url}}\images\2023-04-06-Review0406-DiscreteMathematics\image-20230406095019029.png)



### 관계 행렬 (Relation Matrix)

부울 행렬을 이용하는 방법이다.

부울 행렬이란 행렬 안에 있는 모든 원소들이 0 또는 1로 표시되는 행렬이다

관계 행렬의 행에는 집합 A의 원소, 열에는 집합 B의 원소를 표시한다.

행렬의 각 요소의 값은 a $\in\$ A와 b $\in\$ B의 관계가 있으면 1, 관계가 없으면 0으로 표현한다.

![image-20230406095225384]({{site.url}}\images\2023-04-06-Review0406-DiscreteMathematics\image-20230406095225384.png)



## 합성 관계

세 집합 A, B, C에서 $R_1\$을 집합 A에서 집합 B로의 관계라 하고, 으를 집합 $R_2\$에서 집합 C로의 관계라 하면, 집합 A에서 집합 C로의 합성 관계(composite elation) $R_1\$ • $R_2\$ 또는 $R_1\$$R_2\$는 다음과 같이 정의된다

$R_1\$ • $R_2\$ = {(a, c) $\mid\$ a $\in\$ A, c $\in\$ C, (a, b) $\in\$ $R_1\$이고 (b, c) $\in\$ $R_2\$}

![image-20230406095730216]({{site.url}}\images\2023-04-06-Review0406-DiscreteMathematics\image-20230406095730216.png)

> 집합 A에 대한 항등 관계(Identity relation) $I_A\$는 다음과 같이 정의 된다
>
> $I_A\$ = {(a, a) $\mid\$ a $\in\$ A}



## 관계의 성질

### 반사 관계 (Reflexive Relation)

> 집합 A에 있는 모든 원소 x 대하여 xRx이면, 즉 (x, x) $\in\$ R이면 관계 R을 반사 관계 (reflexive relation)라고 한다.

![image-20230406100111374]({{site.url}}\images\2023-04-06-Review0406-DiscreteMathematics\image-20230406100111374.png)



### 비반사 관계 (Irreflexive Relation)

> 반사 관계와는 반대로 집합 A의 모든 원소에 대하여 a $\in\$ A, (a, a) $\notin\$ R이면 R을 비반사 관계(irreflexive r이ation)라고 한다
>
>  즉, R이 비반사 관계이면 R의 원소 중에는 (a, a), a $\in\$ A인 원소가 하나도 존재하지 않는다.



### 대칭 관계 (Symmetric Relation)

> 집합 A에 있는 원소 x, y에 대해 (x, y) $\in\$ R일 때 (y, x) $\in\$ R이면 관계 R을 대칭 관계(symmetric relations)라고 한다

![image-20230406100456126]({{site.url}}\images\2023-04-06-Review0406-DiscreteMathematics\image-20230406100456126.png)



### 반대칭 관계 (Anti-Symetric Relation)

> 집합 A에 있는 모든 원소 x, y에 대하여(x, y) $\in\$ R이고 (y, x) $\in\$ R일 때 x =y인 관계를 만족하면 관계 R을 반대칭 관계(anti-symmetric relations)라고 한다

> 어떤 경우에는 대칭 관계와 반대칭 관계가 같이 존재할 수도 있다. 
>
> 예를 들어, 尺={(1, 1), (2, 2), (3, 3)}과 같이 각 원소들이 자기 자신에 대한 반사 관계를 가지면서 다른 원소들과 는 대칭의 관계가 없을 경우, 이 관계는 대칭 관계도 되고 반대칭 관계도 성립된다.

![image-20230406100825537]({{site.url}}\images\2023-04-06-Review0406-DiscreteMathematics\image-20230406100825537.png)



### 추이 관계 (Transitive Relation)

> 집합 A에 있는 원소 x, y, z에 대하여 관계 R이 (x, y) $\in\$ R이고 (y, z) $\in\$ R이면 (x, z) $\in\$ R인 관계를 만족할 때 관계 R을 추이 관계(transitive relation)라고 한다

![image-20230406101002744]({{site.url}}\images\2023-04-06-Review0406-DiscreteMathematics\image-20230406101002744.png)



### 클로우저 (Closure)

>  R의 추이 클로우저 $R^+\$= $\underset{n = 1}{\overset{\infty}{\bigcup}}\$는 다음과 같이 정의된다 n = 1 
>
> 1 만약 (a, b) $\in\$ R이면 (a, b) $\in\$ $R^+\$이다. 
> 2 만약 (a, b) $\in\$ $R^+\$이고 (b, c) $\in\$ R이면 (a, c) $\in\$ $R^+\$이다.
> 3 (1), (2)의 경우를 제외하고는 어떤 것도 $R^+\$에 속하지 않는다.

> R*로 표현되는 R의 반사 및 추이 클로우저 (reflexive and transitive closure)는 $R^+\$ $\cup\$ {(a, a) $\mid\$ a $\in\$ S}가 된다



## 동치 관계와 분할

> 관계 R에서 반사 관계, 대칭 관계, 추이 관계가 모두 성립할 때 이를 동치 관계 (equivalence relation)라고 한다. 
>
> 동치 관계 R의 중요한 성질로는 R이 서로 공통 부분이 없으면서 공집합이 아닌 클래스들로 S를 분할한다는 점이다.

> 집합 A에 대한 동치 관계를 R이라고 할 때, A의 각 원소 x에 대하여 [x]를 R에 대한 x의 동치류(equivalence classes) 또는 동치 클래스라 하고 [x] = {y $\mid\$ (x, y) $\in\$ R} 로 정의한다. 
>
> 이때 집합 A의 동치류의 모임을 A의 몫집합(q나otient set)이라 하고, $A \over R\$으로 나타낸다
>
>  $A \over R\$ = {[x] $\mid\$ x $\in\$ A}

> 공집합이 아닌 집합 A의 분할(partitions)이란 다음 조건을 만족시키는 A의 부분 집합의 모임 {$A_1\$，$A_2\$, …，$A_n\$}을 말한다.
>
> 1. $A_i\$ $\ne\$ $\emptyset\$, 1 $\le\$ $i\$ $\le\$ $n\$
> 2. $A\$ =  $\underset{i = 1}{\overset{n}{\bigcup _{A^i}}}\$
> 3. $A_i\$ $\cap\$ $A_j\$ = $\emptyset\$, $i \ne j\$



## 부분 순서 관계

> 집합 A에서의 관계 R $\subseteq\$ A x A는 다음과 같은 성질을 가질 수 있다. 
>
> 1. 반사 관계 : 모든 x $\in\$ A에 대해 xRx이다. 
>
> 2. 반대칭 관계 : 모든 x, y $\in\$ A에 대해"xRy이고 yRx이면 x = y이다. 
>
> 3. 추이 관계 : 모든x, y, z $\in\$ A에 대해"xRy이고 yRz이면 xRz이다. 
>
>
>위의 세 가지 관계를 모두 만족시키는 관계를 부분 순서 관계라고 한다

> 집합 A에 대한 관계 R이 반사 관계, 반대칭 관계, 추이 관계이면 관계 R을 부분 순서 관계 (partially ordered relation)라고 한다. 
>
> 또한 R이 A에 대한 부분 순서 관계이면 순서쌍 (A, R)을 부분 순서 집합(partially order set, Poset)이라고 한다.
>
> A의 두 원소 x, y에 대하여 (x, y) $\in\$ R 을 x $\lesssim\$ y로 표기한다.
>
> x $\lesssim\$ y의 관계인 경우 'x가 y를 선행한다(x precedes y)'라고 읽는다.



 비교 가능(comparable)

 * 부분 순서 집합 (A, $\lesssim\$)에서 집합 A의 두 원소 x, y가 x $\lesssim\$ y 또는 y $\lesssim\$ x이면 x와 y는 비교 가능이라고 한다.

 선형 순서 집합(linearly ordered set)

 * 집합 A의 모든 두 원소가 비교 가능하면 A를 선형 순서 집합이라 한다.

 선형 순서 관계(linearly ordered realation, linear order)

 * 선형 순서 집합인 경우 관계 $\lesssim\$라고 한다.

> 집합 A상에서의 관계 R이 다음 조건을 만족할 경우 선형 순서(linear order)라고 한다. 
>
> 1. R이 부분 순서를 만족한다. 
> 2. 만약 a $\in\$ A, b $\in\$ A라면 aRb, bRa 또는 a=b 중 하나가 성립한다.



### 하세 도표 (Hasse Diagram)

방향 그래프의 일종으로서 화살표는 표시하지 않고 모든 연결선(edge)을 트리 (tree)와 같이 모두 아래 방향을 향하도록 그린다.

하세 도표에 서 모든 순환(loop)은 표시하지 않고 집합 A의 원소 x, y, z에서 x $\lesssim\$ y이고 y $\lesssim\$ z를 만족하는 y가 존재하지 않을 경우에만 x에서 z로의 연결선을 그려 준다.

![image-20230406105618440]({{site.url}}\images\2023-04-06-Review0406-DiscreteMathematics\image-20230406105618440.png)
