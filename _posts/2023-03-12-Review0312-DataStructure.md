---
layout: single
title:  "Chapter 2. 순환"
categories: DataStructure
tag: [자료구조, C언어, 나작복]
toc: true
author_profile: false
sidebar:
    nav: "docs"
search: true #true, false
use_math: true
---

## 2.1 순환의 소개

**순환(recursion)**이란 

어떤 알고리즘이나 함수가 자기 자신을 호출하여 문제를 해결하는 프로그래밍 기법이다.



### 순환의 예

$n! = \begin{cases} 1, \mbox{if }n \mbox{ =0} \\ 

n*(n-1)! \mbox{if }n\mbox{ >=1} \end{cases}\$

```c
int factorial(int n) {
    if(n <= 1)
        return (1);
    else
        return (n*factorial(n-1));
}
```

만약 factorial(3)을 호출했을 경우 수행 도중에 factorial(2)를 호출하게 되고 factorial(2)는 다시 factorial(1)을 호출하게 된다.

factorial(1)은 n이 1이므로 첫 번째 if 문장이 참이 되고 따라서 순환 없이 1을 반환하게 된다.



### 순환 호출의 내부적인 구현

위와 같은 프로그램이 동작할 때 어떤 과정을 거칠까?

먼저 **복귀주소**가 시스템 스택에 저장되고 호출되는 함수를 위한 **매개변수(parameter)**와 **지역변수**를 스택으로부터 할당받는다.

이러한 함수를 위한 시스템 스택에서의 공간을 **활성 레코드(activation record)**라 한다.

준비가 끝나면 호출된 함수의 시작 위치로 점프하여 수행을 시작한다. 

만약 호출된 함수가 자기 자신이라면 자기 자신의 시작 위치로 점프하게 된다.

이후 호출된 함수가 끝나게 되면 시스템 스택에서 복귀주소를 추출하여 호출한 함수로 되돌아가게 된다.



### 순환 알고리즘의 구조

순환 알고리즘은 자기 자신을 호출하는 부분과 순환 호출을 멈추는 부분으로 구성되어 있다.

만약 순호나 호출을 멈추는 부분이 없다면 시스템 스택을 다 사용할 때까지 순환적으로 호출되다가 오류를 내면서 멈출 것이다.

**따라서 반드시 순환 호출에는 순환 호출을 멈추는 문장이 포함되어야 한다.**



### 순환 **$\leftrightarrow\$** 반복

**반복(iteration)**이란

for나 while 등의 반복구조로 간명하고 효율적으로 되풀이 하는 방법이다.

반면에 반복을 사용하게 되면 지나치게 복잡해지는 문제들도 존재한다.

이런 경우 순환이 좋은 해결책이 될 수 있다.



기본적으로 반복과 순환은 문제 해결 능력이 같으며 많은 경우에는 순환 알고리즘을 반복 버전으로, 반복 알고리즘을 순환 버전으로 바꾸어 쓸 수 있다.

다음은 위 순환을 이용한 factorial함수를 반복 버전으로 바꾼 형태이다.

```c
int factorial_iter(int n) {
    int i, result = 1;
    for (i=1; i<=n; i++)
        result *= i;
    return (result);
}
```

순환과 반복 중에서 어떤 형태가 더 좋을까?

문제의 정의가 순환적으로 되어 있는 경우 순환으로 작성하는 것이 훨씬 더 쉽다.

또한 대개 순환 형태의 코드가 더 이해하기 쉽다.

그러나 순환적인 코드의 약점은 실행 시간에 있다.

따라서 무엇이 더 좋다기보다는 수행 시간, 기억 공간 등을 고려하여 더 이로운 것을 선택하는 것이 바람직하다.

예시로 factorial의 경우 순환을 사용했을 때와 반복을 사용했을 때 $O(n) = n$으로 동일하지만 순환 호출의 경우 여분의 기억 공간이 더 필요하고 함수를 호출하기 위해서는 함수의 매개변수들을 스택에 저장하는 등의 사전 작업이 상당히 필요하다.

그러나 거듭제곱값 계산의 경우 순환을 사용했을 때 반복을 사용했을 때보다 수행 시간이 짧다.



## 2.2 거듭제곱값 계산

```c
double power_iter(double x, int n) {
    int i;
    double result = 1.0;
    
    for(i=0; i<n; i++)
        result *= x;
    return result;
}
```

```c
double power_recursion(double x, int n) {
	1f( n==0 ) 
        return 1;
	else if ( (n%2)==0 )
		return power(x*x, n/2);
	else 
        return x*power(x*x, (n-l)/2);
}
```

함수 power_iter의 경우 시간 복잡도가 $O(n)\$이다.

함수 power_recursion의 경우 처음에는 n승 이었다가 n/2승으로, 또 n/4승으로 크기가 점점 줄어든다.

$n = 2^k\$라고 가정하자

양변에 $log\$를 취하면 $log_{2} n = k\$임을 알 수 있다.

따라서 시간 복잡도는 $O(log_{2} n)\$으로 반복을 사용한 경우보다 순환을 사용했을 때 더욱 빠른 것을 알 수 있다.



## 2.3 피보나치 수열의 계산

순환을 사용하게 되면 단순하게 작성이 가능하며 가독성이 높아진다.

그러나 중복된 계산을 몇 번씩 반복한다면 계산시간이 엄청 길어질 수 있다.

```c
int fib(int n) {
	if( n==0 ) 
        return 0;
	if( n==l ) 
        return 1;
	
    return (fib(n-l) + fib(n-2));
}
```

위의 함수는 단순하지만 중복되는 계산이 반복되기 때문에 비효율적이다.

![image-20230312213132321]({{site.url}}\images\2023-03-12-Review0312-DataStructure\image-20230312213132321.png)

$T(n) = T(n-1) + T(n-2) + C\$이고 $O(2^n)\$을 가지는 걸 알 수 있다.

```c
int fib_iter(int n) {
	if (n == 0) 
        return 0;
	if (n == 1) 
        return 1;
	int pp = 0;
	int p = 1;
	int result = 0;
	for (int 1 = 2; i <= n; i++) {
		result = p + pp;
		PP = P；
		p = result;
	}
	return reult;
}
```

순환을 사용하지 않고 반복구조를 이용하면 $O(n)\$이라는 계산시간이 훨씬 짧은 알고리즘을 구성할 수 있다.



## 2.4 하노이탑 문제

순환을 가장 잘 이용할 수 있는 것은 하노이탑 문제이다.

```c
#include <stdio.h>
void hanoi_tower(int n, char from, char tmp, char to) {
	if (n == 1) 
        printf("원판 1을 %c 에서 %c으로 옮긴다.\n", from, to);
	else {
		hanoi_tower(n—1, from, to, tmp);
		printf("원판 %d을 %c에서 %c으로 옮긴다.\n", n, from, to);
		hano1_tower(n-1, tmp, from, to);
	}
}

int main(void) {
	hanoi_tower(4, 'A', 'B', 'C');
	return 0;
}
```

