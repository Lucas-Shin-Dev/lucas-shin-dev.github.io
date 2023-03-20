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

$a_5\$*$a_4\$*$a_3\$*$a_2\$*$a_1\$*$a_0\$*$a_{-1}\$*$a_{-2}\$*$a_{-3}\$ 

= $a_5\$*$r^5\$+$a_4\$*$r^4\$+$a_3\$*$r^3\$+$a_2\$*$r^2\$+$a_1\$*$r^1\$+$a_0\$*$r^0\$+$a_{-1}\$*$r^{-1}\$+$a_{-2}\$*$r^{-2}\$+$a_{-3}\$*$r^{-3}\$

산술 연산은 decimal(10진법)과 같은 규칙으로 연산한다.



## Number-base conversions

decimal $ \rightarrow r \$로 변환하려면 숫자와 모든 연속적인 몫을 r로 나누고 나머지를 모으면 된다.

decimal의 소수는 나누는 대신 1만 남을 때까지 곱한다. 



### 2 number system

2진수는 10진수로 나타낸 수에 2로 나누거나 곱하여 구할 수 있다.



![image-20230317125818108]({{site.url}}\images\2023-03-15-DigitalDesign0315\image-20230317125818108.png)![image-20230317125838697]({{site.url}}\images\2023-03-15-DigitalDesign0315\image-20230317125838697.png)

따라서 $(41.06875)_{10} \$는 2진수로 변환하면 $(101001.1011)_2$로 나타낼 수 있다.



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

 1. $M \ge N\$이면 결과는 M - N, end carry $r^n\$은 버린다.

 2. $M<N\$이면 결과는 $r^n-(N-M)\$ 즉 $(N-M)\$의 r's complement를 취한 뒤 (-)를 붙인다.

     

### (r-1)'s Complement를 이용하는 방법

$M + ((r^n-1)-N) = (M - N) + (r^n-1)\$ (피감수 M, 감수 N)

 1. $M \ge N\$이면 결과는 M - N, end carry $r^n\$은 버린 후 1을 더해준다.(이를 end around carry라고 한다.)

 2. $M<N\$이면 결과는 $(r^n-1)-(N-M)\$ 즉 $(N-M)\$의 (r-1)'s complement를 취한 뒤 (-)를 붙인다.

    



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

$0101 \rightarrow 5\$

$1101 \rightarrow -5\$

이 표현법의 단점은 0의 중복이다.(0000과 1000은 +0과 -0으로 동일하다.)

즉 -7 ~ +7로 총 15개의 표현이 가능하다.

또한 일반적인 산술 연산을 할 경우 부호 비트와 크기 비트를 나눠야해서 불편하다.



### Signed 1's Complement Representation

양수를 나타내는 비트에 1's complement를 취하여 음수를 나타낸다.

$0101 \rightarrow 5\$

$1010 \rightarrow -5\$

이 표현법은 논리 연산에 유용하지만 Signed Magnitude Representation과 동일하게 0의 중복이다.(0000과 1111은 +0과 -0으로 동일하다.)

즉 -7 ~ +7로 총 15개의 표현이 가능하다.



### Signed 2's Complement Representation

양수를 나타내는 비트에 2's complement를 취하여 음수를 나타낸다.

$0101 \rightarrow 5\$

$1011 \rightarrow -5\$

이 표현법은 논리 연산에 유용할 뿐만아니라 Signed Magnitude Representation과 Sigend 1's Complement Representation과 다르게 0의 중복이 발생하지 않는다.

즉 -8 ~ +7로 총 16개의 표현이 가능해 일반적으로 사용된다.

![image-20230317125928529]({{site.url}}\images\2023-03-15-DigitalDesign0315\image-20230317125928529.png)

### Arithmetic Addition & Subtraction

Signed Magnitude System에서는 일반적인 산술 연산과 동일하다.

Signed Complement System에서는 오직 덧셈만 가능하다.

A - B = A + (-B)이므로 B에 complement를 취해 A와 더해주면 덧셈만 사용했지만 뺄셈을 한 것과 같다. 



## Binary Code

### BCD code (Binary Coded Decimal)

Decimal 수의 각 자리 숫자를 4bit의 Binary로 나타낸다.

Decimal의 0 ~ 9 를 나타내기 위해 Binary의 0000 ~ 1001만 사용하고 1010 ~ 1111은 사용하지 않는다.

$(4634)_{10}\$는 $(0100 0110 0011 0100)_2\$로 나타낼 수 있다.



### BCD Addition

Binary 합이 0000 ~ 1001 사이라면 BCD의 자릿수는 올바르다.

그러나 1010보다 크거나 같은 경우 유효하지 않는다.

이를 보정하기 위해 decimal의 올림수 차이가 6이기 때문에 $6_{10} = 0110_2\$를 더해준다.

그러면 올바른 자릿수로 변환되며 필요에 따라 올림수가 생성된다.



### Other codes

![image-20230317130006628]({{site.url}}\images\2023-03-15-DigitalDesign0315\image-20230317130006628.png)

2421과 Excess-3(3초과) code는 자기 보수화 코드로 0과 9, 1과 8, ... , 4와 5가 보수화되어 있다.

8421(BCD), 2421은 가중 코드로 각 자리에 가중치를 곱한 값이다.

2421의 경우 $6_{10}\$을 나타내는 $1100_2\$은 1x2 + 1x4 + 0x2 + 0x1로 계산하여 6을 나타낸다.

반면 Excess-3 code의 경우 BCD(8421)에 3을 더한 비가중 코드이다.



### Gray Code

![image-20230317130026136]({{site.url}}\images\2023-03-15-DigitalDesign0315\image-20230317130026136.png)

Gray Code는 인접한 두 수의 XOR(Exclusive OR) 값으로 나타낸다.

Binary Code 0 1 1 1을 예로 들어 설명하면 최상위 비트는 그대로 두고 왼쪽부터 인접한 두 수의 XOR값을 적는다.

따라서 Gray Code 0 1 0 0 으로 변환된다.

역으로 Gray Code 0 1 0 0을 Binary Code로 변환하려면 최상위 비트는 그대로 두고 그 비트와 Gray Code의 다음 수와 XOR 결과값을 적고 그 결과값과 Gray Code의 그 다음 비트와 또 XOR연산을 한다.

따라서 Binary Code 0 1 1 1로 다시 변환된다.



Gray Code의 장점은 Binary의 인접한 두 수는 오직 1bit만 차이가 난다.

따라서 오류 발생시 다른 Code보다 더 작은 에러를 발생시킬 수 있다.



### ASCII Character Code

![image-20230317131039652]({{site.url}}\images\2023-03-15-DigitalDesign0315\image-20230317131039652.png)

ASCII Code는 94개의 인쇄문자와 34의 제어문자로 이루어져있다.

제어문자는 형식 지정자, 정보 구분 기호, 통신 제어 문자 3가지로 구성되어있다.

대문자와 소문자는 6번째 비트의 차이만 있고 다른 비트는 모두 동일하다.



### Error Detectiong Code

Even Parity는 1의 개수를 짝수로, Odd Parity는 1의 개수를 홀수로 만들기 위해 코드의 가장 왼쪽 위치(약속에 따라 변경 가능)에 여분의 비트를 추가한다.

ASCII A = 1000001일 때, Even Parity는 01000001로, Odd Parity는 11000001로 나타낸다.

ASCII T = 1010100일 때, Even Parity는 01010100로, Odd Parity는 11010100로 나타낸다.

Binary Logic으로 Parity Bit를 나타내려면 코드를 모두 XOR(Exclusive OR)연산을 하면 된다.

1의 개수가 짝수일 때 XOR 결과는 0이고 홀수일 때 XOR 결과는 1이다.

$P_{even}\$= $D_1\$ $\oplus\$ $D_2\$ $\oplus\$ $D_3\$ $\oplus\$ $D_4\$ $\oplus\$ $D_5\$ $\oplus\$ $D_6\$ $\oplus\$ $D_7\$

$P_{odd}\$는 $P_{even}\$에 NOT 연산을 하면 된다.

따라서 다음 그림과 같이 이용할 수 있다.

$Y_{even}\$= $P_{even}\$ $\oplus\$ $D_1\$ $\oplus\$ $D_2\$ $\oplus\$ $D_3\$ $\oplus\$ $D_4\$ $\oplus\$ $D_5\$ $\oplus\$ $D_6\$ $\oplus\$ $D_7\$

Y가 0이라면 오류 없음, 1이라면 오류 발생을 뜻한다.

![image-20230319200737541]({{site.url}}\images\2023-03-15-DigitalDesign0315\image-20230319200737541.png)



Parity bit는 임의의 홀수 개의 오류는 검출 가능하나 임의의 짝수 개의 오류는 검출이 불가능하다.

또한 오류를 검출했더라도 어느 위치에서 오류가 발생했는지 알 수 없다.

이를 보완한게 Parallel Parity이다.

1차원 배열을 2차원 배열로 변경하므로써 어느 위치에서 오류가 발생했는지 알 수 있게 되었다. 

![image-20230319201157763]({{site.url}}\images\2023-03-15-DigitalDesign0315\image-20230319201157763.png)



## Binary Logic

![image-20230319201905162]({{site.url}}\images\2023-03-15-DigitalDesign0315\image-20230319201905162.png)

1. AND: 이 연산은 점（ • ） 또는 연산자 생략으로 표시된다. 예를 들어 x • y = z 또는 xy = z는 "x AND y는 그와 같다”로 읽는다. 논리 연산 AND는 x = 1이고 y = 1일 경우에 만 z = 1이며 그 밖의 경우에는 z = 0을 의미하는 것으로 해석된다. （x, y 및 z는 2진 변 수이고 1 또는 0과 같을 수 있으며 다른 것일 수는 없음을 기 억하라.） x • y 연산의 결과는 z이다.

2. OR: 이 연산은 더하기 기호로 표시된다. 예를 들어 x + y = z는 "x OR y는 z와 같다” 로 읽는다. x = 1인 경우 또는 y = 1인 경우 또는 X = 1 및 y = 1인 경우 Z = 1임을 의 미한다. x = 0이고 y = 0이면 z = 0이다. 

3. NOT: 이 연산은 프라임으로（때때로 오버 바로） 표시된다. 예를 들어 x' = z 는 “X의 부정은 z와 같다”로 읽는다. 그는 X가 아닌 것을 의미한다. 즉, X = 1이면 Z = 0이 지만 x = 0이면 z = 1이다. NOT 연산은 보수 연산이라고도 하는데, 1은 0으로 0은 1로 변경하기 때문이다. 즉, 1을 보수화한 결과는 0이며 그 반대의 경우도 성립한다.
