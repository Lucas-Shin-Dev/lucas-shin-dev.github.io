---
layout: single
title:  "Chapter 3. 배열, 구조체, 포인터"
categories: DataStructure
tag: [자료구조, C언어, 나작복]
toc: true
author_profile: false
sidebar:
    nav: "docs"
search: true #true, false
use_math: true
---



## Array (배열)

배열을 사용하면 **연속적인 메모리 공간**이 할당되고 인덱스 번호를 사용하여 쉽게 접근이 가능하기 때문에 여러 가지 작업을 손쉽게 할 수 있다.



### 배열 ADT

```
객체: <인덱스, 값> 쌍의 집합
연산:
	create(size) ::= size개의 요소를 저장할 수 있는 배열
	get(A, i) ::= 배열 A의 i번째 요소 반환
	set(A, i, v) ::= 배열 A의 i번째 위치에 값 v 저장
```

c언어에서는 배열이 기본적으로 제공되기 때문에 위의 연산을 직접 구현할 필요가 없으나 기본적으로 제공하지 않는다면 직접 구현해야 한다.

### C언어에서의 배열

```c
//1차원
int list[6];	//create 연산
list[0] = 100;	//set 연산
value = list[0];	//get 연산

//2차원
int list[3][5];	//create 연산
list[1][3] = 4;	//set 연산
value = list[1][3];	//get 연산
```



## Structure (구조체)

복잡한 객체에는 다양한 타입의 데이터들이 한데 묶여져 있다.

배열은 타입이 같은 데이터의 모임이라면 구조체는 타입이 다른 데이터의 모임이다.

```c
//(이름 없는) 구조체 형식 정의
struct 구조체이름 {
    항목1;
    항목2;
};

//구조체 변수 생성
struct 구조체이름 구조체변수;
```



간단한 예시로 구조체를 만들어보면

```c
struct studentTag {
    char name[10];
    int age;
    double grade_average;
};

struct studentTag s1;

strcpy(s1.name, "Kim");
s1.age = 23;
s1.grade_average = 4.0;
```

구조체 안에 들어 있는 멤버를 사용하려면 변수 뒤에 **'.'**을 첨가한 후 항목 이름을 적으면 된다.

이때 **'.'**을 멤버 연산자(membership operator)라고 한다.



C언어에서는 typedef을 사용하여 구조체를 새로운 타입으로 선언하는 것이 가능하다.

또한 중괄호를 사용하여 선언 시에 초기화하는 것이 가능하다.

```c
typedef studentTag {
    char name[10];
    int age;
    double grade_average;
} student;

student s1 = {"Kim", 23, 4.0};
```



## 배열의 응용: 다항식

$P(x)\$ = $a_n\$$x^n\$ + $a_{n-1}\$$x^{n-1}\$ + ... + $a_1\$$x^1\$ + $a_0\$$x^0\$

위의 다항식에서 a: 계수, $x\$: 변수, $n\$: 차수라 부른다.

프로그램 안에서 표현하려면 두 가지 방법이 있다.



### 첫 번째 방법

모든 차수의 계수값을 배열에 저장하는 것이다.

10$x^5\$ + 6$x\$ + 3의 모든 차수에 대한 계수값들의 리스트인 (10, 0, 0, 0, 6, 3)을 배열 coef에 저장하는 것이다.

```c
#define MAX_DEGREE 101

typedef struct {
    int degree;
    float coef[MAX_DEGREE];
} polynomial;

polynomial a = {5, (10, 0, 0, 0, 6, 3)};
```

이 방법은 간단하고 쉽게 이해가 되어 알고리즘이 간단하다.

하지만 대부분의 항이 0인 경우 **공간의 낭비가 심하다**는 단점이 있다.



이 방법으로 프로그램을 만들어보면

```c
#include <stdio.h>
#define MAX(a,b) (((a)>(b)) ?(a):(b))
#define MAX_DEGREE 101

typedef struct {
	int degree;	//차수
	float coef[MAX_DEGREE];	//계수
}polynomial;

polynomial poly_add1(polynomial A, polynomial B) {
	polynomial C;	//결과 다항식
	int Apos = 0, Bpos = 0, Cpos = 0;	//배열 인덱스 변수
	int degree_a = A.degree;
	int degree_b = B.degree;

	C.degree = MAX(A.degree, B.degree);	//결과 다항식 차수
	
	while (Apos <= A.degree && Bpos <= B.degree) {
		if (degree_a > degree_b) {	//A항 차수 > B항 차수
			C.coef[Cpos++] = A.coef[Apos++];	//A항 계수를 C항에 
			degree_a--;	//A항 차수를 1내림
		}
		else if (degree_a == degree_b) {	//A항 차수 == B항 차수
			C.coef[Cpos++] = A.coef[Apos++] + B.coef[Bpos++];	//A항 계수 + B항 계수
			degree_a--;	//A항 차수를 1내림
			degree_b--;	//B항 차수를 1내림
		}
		else {	//A항 차수 < B항 차수
			C.coef[Cpos++] = B.coef[Bpos++];	//B항 계수를 C항에 
			degree_b--;	//B항 차수를 1내림
		}
	}
	return C;
}

void print_poly(polynomial p) {
	for (int i = p.degree; i > 0; i--) {
		if (p.coef[p.degree - i] == 0) {	//계수가 0이면 빈값 출력
			printf("");
		}
		else {
			printf("%3.1fx^%d + ", p.coef[p.degree - i], i);
		}
	}
	printf("%3.1f \n", p.coef[p.degree]);
}

int main(void) {
	polynomial a = { 5, {3, 6, 0, 0, 0, 10} };
	polynomial b = { 5, {-3, 7, 0, 5, 0, 1} };
	polynomial c;

	print_poly(a);
	print_poly(b);
	c = poly_add1(a, b);
	printf("--------------------------------------------------\n");
	print_poly(c);
	return 0;
}
//결과
//3.0x^5 + 6.0x^4 + 10.0
//-3.0x^5 + 7.0x^4 + 5.0x^2 + 1.0
//--------------------------------------------------
//13.0x^4 + 5.0x^2 + 11.0
```



### 두 번째 방법

공간을 절약하기 위해 0이 아닌 항만 하나의 전역 배열에 저장하는 방법이다.

0이 아닌 항들을 (계수, 차수)의 형식으로 구조체 배열에 저장된다.

즉 10$x^5\$ + 6$x\$ + 3는 ((10, 5), (6, 1), (3,0))으로 표시하는 것이다.



```c
#define MAX_TERMS 101
struct {
    float coef;
    int expon;
} terms[MAX_TERMS];

int avail;
```

$A\$ = $8x^3\$ + $7x\$ + 1,		$B\$ = $10x^3\$ + $3x^2\$ + 1

![image-20230402143412088](C:\blogmaker\images\2023-04-02-Review0402-DataStructure\image-20230402143412088.png)

이러한 방법은 terms 안에 항의 총 개수가 MAX_TERMS을 넘지만 않으면 많은 다항식을 저장할 수 있다.

그러나 이 방식은 하나의 다항식이 시작되고 끝나는 위치를 가리키는 인덱스 변수들을 관리하여야 한다.

또한 차수도 저장해야 하기 때문에, 다항식에 따라서는 첫번째 방법보다 더 많은 공간을 필요로 할 수도 있다.

그리고 다항식 연산들의 구현이 어려워진다.



이 방법으로 프로그램을 만들어보면

```c
#include <stdio.h>
#include <stdlib.h>
#define MAX_TERMS 101

typedef struct {
	float coef;
	int expon;
} polynomial;

polynomial terms[MAX_TERMS] = { {8, 3}, {7,1}, {1,0},{10,3},{3,2},{1,0} };
int avail = 6;

//두 개의 정수 비교
char compare(int a, int b) {
	if (a > b) {
		return '>';
	}
	else if (a == b) {
		return '=';
	}
	else {
		return '<';
	}
}

void attach(float coef, int expon) {
	if (avail > MAX_TERMS) {
		fprintf(stderr, "항의 개수가 많음\n");
		exit(1);
	}
	terms[avail].coef = coef;
	terms[avail].expon = expon;
	avail++;
}

void poly_add2(int As, int Ae, int Bs, int Be, int* Cs, int* Ce) {
	float tempcoef;
	*Cs = avail;
	while (As <= Ae && Bs <= Be) {
		switch (compare(terms[As].expon, terms[Bs].expon)) {
		case '>':
			attach(terms[As].coef, terms[As].expon);
			As++;
			break;
		case '=':
			tempcoef = terms[As].coef + terms[Bs].coef;
			if (tempcoef) {
				attach(tempcoef, terms[As].expon);
			}
			As++;
			Bs++;
			break;
		case '<':
			attach(terms[Bs].coef, terms[Bs].expon);
			Bs++;
			break;
		}
	}
	for (; As <= Ae; As++) {
		attach(terms[As].coef, terms[As].expon);
	}
	for (; Bs <= Be; Bs++) {
		attach(terms[Bs].coef, terms[Bs].expon);
	}
	*Ce = avail - 1;
	
}

void print_poly(int s, int e) {
	for (int i = s; i < e; i++) {
		printf("%3.1fx^%d + ", terms[i].coef, terms[i].expon);
	}
	printf("%3.1fx^%d\n", terms[e].coef, terms[e].expon);
}

int main(void) {
	int As = 0, Ae = 2, Bs = 3, Be = 5, Cs, Ce;
	poly_add2(As, Ae, Bs, Be, &Cs, &Ce);
	print_poly(As, Ae);
	print_poly(Bs, Be);
	printf("--------------------------------------------------------\n");
	print_poly(Cs, Ce);
	return 0;
}
```



## 배열의 응용: 희소행렬

배열을 이용하여 행렬을 표현하는 방법은 2 가지가 있다.

### 첫 번째 방법

2 차원 배열을 이용하여 배열 전체 요소를 저장하는 방법

장점: 행렬의 연산들을 간단하게 구현할 수 있다.

단점: 대부분의 항들이 0인 희소 행렬의 경우 많은 메모리 공간 낭비가 심하다.

```c
#include <stdio.h>
#define ROWS 3
#define COLS 3

void sparse_matrix_add1(int A[ROWS][COLS], int B[ROWS][COLS], int C[ROWS][COLS]) {
	int r, c;
	for (r = 0; r < ROWS; r++) {
		for (c = 0; c < COLS; c++) {
			C[r][c] = A[r][c] + B[r][c];
		}
	}
}

void main() {
	int array1[ROWS][COLS] = { {2,3,0},{8,9,1},{7,0,5} };
	int array2[ROWS][COLS] = { {1,0,0},{1,0,0},{1,0,0} };
	int array3[ROWS][COLS];

	sparse_matrix_add1(array1, array2, array3);
}
```



### 두 번째 방법

0이 아닌 요소들만 저장하는 방법

장점: 희소 행렬의 경우, 메모리 공간을 절약할 수 있다.

단점: 각종 행렬 연산들의 구현이 복잡해진다.

```c
#include <stdio.h>
#define ROWS 3
#define COLS 3
#define MAX_TERMS 10

typedef struct {
	int row, col, value;
}element;

typedef struct SparseMatrix {
	element data[MAX_TERMS];
	int rows;
	int cols;
	int terms;
}SparseMatrix;

SparseMatrix sparse_matrix_add2(SparseMatrix a, SparseMatrix b) {
	SparseMatrix c;
	int ca = 0, cb = 0, cc = 0;

	if (a.rows != b.rows || a.cols != b.cols) {
		fprintf(stderr, "희소행렬 크기 에러\n");
		exit(1);
	}
	c.rows = a.rows;
	c.cols = a.cols;
	c.terms = 0;

	while (ca < a.terms && cb < b.terms) {
		int inda = a.data[ca].row * a.cols + a.data[ca].col;
		int indb = b.data[cb].row * b.cols + b.data[cb].col;
		
		if (inda < indb) {
			c.data[cc++] = a.data[ca++];
		}
		else if (inda == indb) {
			c.data[cc].row = a.data[ca].row;
			c.data[cc].col = a.data[ca].col;
			c.data[cc++].value = a.data[ca++].value + b.data[cb++].value;
		}
		else {
			c.data[cc++] = b.data[cb++];
		}
	}
	for (; ca < a.terms; ca++) {
		c.data[cc++] = a.data[ca++];
	}
	for (; cb < b.terms; cb++) {
		c.data[cc++] = b.data[cb++];
	}
	c.terms = cc;
	return c;
}

void main() {
	SparseMatrix m1 = { {{1,1,5},{2,2,9}}, 3,3,2 };
	SparseMatrix m2 = { {{0,0,5},{2,2,9}}, 3,3,2 };
	SparseMatrix m3;

	m3 = sparse_matrix_add2(m1, m2);
}
```



## Pointer (포인터)

포인터는 다른 변수의 주소를 가지고 있는 변수이다.

```c
int a = 100;	//정수형 변수 a 정의
int *p;	//정수형을 가리키는 포인터 p
p = &a;	//a의 주소를 p에 대입, 변수의 주소는 &연산자를 변수에 적용시켜서 추출
```

* &연산자 : 주소 연산자, 변수의 주소를 추출하는 연산자
* *연산자: 간접 참조 연산자(역참조 연산자), 포인터가 가리키는 장소에 값을 저장하는 연산자

```c
int a;
p = $a;
*p = 200;
```

![image-20230402151231392](C:\blogmaker\images\2023-04-02-Review0402-DataStructure\image-20230402151231392.png)



즉, *p 와 a는 전적으로 동일하다. 따라서 *p의 값을 변경하게 되면 a의 값도 바뀌게 된다.



### 다양한 포인터

```c
int *p;	//int형 변수를 가리키는 포인터
float *pf;	//float형 변수를 가리키는 포인터
char *pc;	//char형 변수를 가리키는 포인터
int **pp	//포인터를 가리키는 포인터
struct test *ps //test 타입의 구조체를 가리키는 포인터
void (*f)(int);	//f는 함수를 가리키는 포인터

void *p;
pi = (int*)p;	//필요할 때마다 형변환 가능

//NULL 포인터
if ( p == NULL) {
    fprintf(stderr, "오류: 포인터가 아무 것도 가리키지 않습니다.");
    return;
}
```

포인터를 사용하기 전에는 반드시 널 포인터 인지를 검사해야 한다.

포인터가 아무 것도 가리키고 있지 않을 때는 항상 널 포인터 상태로 만들어 두는 것이 좋다.

널 포인터를 가지고 간접 참조하려고 하면 컴퓨터 시스템에서 오류가 발생되어서 쉽게 알 수 있기 때문이다.

잘못된 포인터를 가지고 메모리를 변경하는 것은 치명적인 결과를 가져올 수 있다.



### 함수 매개변수로 포인터 사용하기

변수 2개의 값을 서로 바꾸는 swap() 함수를 포인터를 이용하여 작성

```c
#include <stdio.h>

void swap(int* px, int* py) {
	int tmp;
	tmp = *px;
	*px = *py;
	*py = tmp;
}

int main(void) {
	int a = 1, b = 2;
	printf("swap을 호출하기 전: a=%d, b=%d\n", a, b);
	swap(&a, &b);
	printf("swap을 호출하기 후: a=%d, b=%d\n", a, b);
	return 0;
}
```



### 배열과 포인터

```c
#include <stdio.h>
#define SIZE 6

void get_integers(int list[]) {
	printf("6개의 정수를 입력하시오: ");
	for (int i = 0; i < SIZE; i++) {
		scanf_s("%d", &list[i]);
	}
}

int cal_sum(int list[]) {
	int sum = 0;
	for (int i = 0; i < SIZE; ++i) {
		sum += *(list + i);
	}
	return sum;
}

int main(void) {
	int list[SIZE];
	get_integers(list);
	printf("합= %d \n", cal_sum(list));
	return 0;
}
```



## 동적 메모리 할당

C언어에서는 필요한 만큼의 메모리를 운영체제로부터 할당 받아서 사용하고, 사용이 끝나면 시스템에 메모리를 반납하는 기능이 있다. 이것을 **동적 메모리 할당**이라고 한다.



동적 메모리가 할당되는 공간을 히프(heep)라고 한다. 히프는 운영체제가 사용되지 않는 메모리 공간을 모아 놓은 곳이다.

필요한 만큼만 할당을 받고 또 필요할 때에 사용하고 반납하기 때문에 메모리를 매우 효율적으로 사용할 수 있다.

```c
int *p;
p = (int*)malloc(sizeof(int));	//동적 메모리 할당
*p = 1000;	//동적 메모리 사용
free(p);	//동적 메모리 반납

(void*)realloc(void* ptr, size_t size);	//기존 ptr의 크기를 size로 변경 후 재 할당하여 주소 반환
(void*)memset(void* ptr, int n, size_t size);	//ptr이 가리키는 할당된 메모리에 n으로 size개 채움
(void*) calloc(size_t size, size_t n)	//size bite 크기를 n개 만큼 할당하고 0으로 초기화하여 주소 반환
```



동적 메모리 할당의 예)

```c
#include <stdio.h>
#include <stdlib.h>
#include <malloc.h>

#define SIZE 10

int main(void) {
	int* p;

	p = (int*)malloc(SIZE * sizeof(int));
	if (p == NULL) {
		fprintf(stderr, "메모리가 부족해서 할당할 수 없습니다.\n");
		exit(1);
	}

	for (int i = 0; i < SIZE; i++) {
		p[i] = i;
	}
	for (int i = 0; i < SIZE; i++) {
		printf("%d ", p[i]);
	}

	free(p);
	return 0;
}
```



### 구조체와 포인터

구조체에 대한 포인터를 선언하고 포인터를 통하여 구조체 멤버에 접근할 수 있다.

구조체의 멤버에 접근하는 편리한 표기법 "->"이 있다.

ps가 구조체를 가리키는 포인터라고 할 때, (*ps).i 보다 ps->i라고 쓰는 것이 더 편리하다.

자료구조에서 구조체에 대한 포인터도 자주 함수의 매개변수로 전달된다.

구조체 자체를 함수로 전달하는 경우, 구조체가 함수로 복사되어 전달되기 때문에, 큰 구조채의 경우에는 구조체 포인터를 전달하는 것이 좋다.



```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct studentTag {
	char name[10];
	int age;
	double gpa;
}student;

int main(void) {
	student* s;

	s = (student*)malloc(sizeof(student));
	if (s == NULL) {
		fprintf(stderr, "메모리가 부족해서 할당할 수 없습니다.\n");
		exit(1);
	}

	strcpy_s(s->name, sizeof(student), "Park");
	s->age = 20;

	printf("%s %d", s->name, s->age);
	free(s);
	return 0;
}
```

