---
layout: single
title:  "Chapter 4. 스택"
categories: DataStructure
tag: [자료구조, C언어, 나작복]
toc: true
author_profile: false
sidebar:
    nav: "docs"
search: true #true, false
use_math: true
---



## Stack (스택)

후입선출(LIFO: Last In First Out)로 가장 나중에 들어온 데이터가 가장 먼저 나간다.

스택의 맨 위에서만 입출력이 일어나고 중간에서는 데이터를 삭제할 수 없다.

![image-20230402183807353]({{site.url}}\images\2023-04-03-Revuew0403-DataStructure\image-20230402183807353.png)

스택에서 입출력이 이루어지는 부분을 스택 상단 (stack top)이라 하고

반대쪽 바닥 부분을 스택 하단 (stack bottom)이라고 한다.

스택에 저장되는 것을 요소 (element)라 한다.

스택에 요소가 하나도 없을 때 그러한 스택을 공백 스택 (empty stack)이라고 한다.



### 스택 ADT

```
객체: 0개 이상의 원소를 가지는 유한 선형 리스트
연산:
	create(size) ::= 최대 크기가 size인 공백 스택을 생성한다.
	is_full(s) ::=
		if(스택의 원소수 == size) return TRUE;
		else return FALSE;
	is_empty(s) ::=
		if(스택의 원소수 == 0) return TRUE;
		else return FALSE;
	push(s, item) ::=
		if(if_full(s)) return ERROR_STACKFULL;
		else 스택의 맨 위에 item을 추가한다.
	pop(s) ::=
		if (is_empty(s)) return ERROR_STACKEMPTY;
		else 스택의 맨 위의 원소를 제거해서 반환한다.
	peek(s) ::=
		if (is_empty(s)) return ERROR_STACKEMPTY;
		else 스택의 맨 위의 원소를 제거하지 않고 반환한다.
```



### 스택 구현

```c
#include <stdio.h>
#include <stdlib.h>
#define MAX_STACK_SIZE 100

typedef int element;

typedef struct {
	element data[MAX_STACK_SIZE];
	int top;
}StackType;

//intialization
void init_stack(StackType* s) {
	s->top = -1;
}

//is_full
int is_full(StackType* s) {
	return (s->top == MAX_STACK_SIZE - 1);
}

//is_empty
int is_empty(StackType* s) {
	return (s->top == -1);
}

//push
void push(StackType* s, element item) {
	if (is_full(s)) {
		fprintf(stderr, "포화상태\n");
	}
	s->data[++(s->top)] = item;
}

//pop
element pop(StackType* s) {
	if (is_empty(s)) {
		fprintf(stderr, "공백상태\n");
		exit(1);
	}
	else {
		return s->data[(s->top)--];
	}
}

//peek
element peek(StackType* s) {
	if (is_empty(s)) {
		fprintf(stderr, "공백상태\n");
		exit(1);
	}
	else {
		return s->data[s->top];
	}
}

int main(void) {
	StackType s;

	init_stack(&s);
	
	push(&s, 1);
	push(&s, 4);
	push(&s, 2);
	push(&s, 6);
	push(&s, 9);
	push(&s, 4);
	push(&s, 7);


	printf("%d\n", pop(&s));
	printf("%d\n", pop(&s));
	printf("%d\n", peek(&s));
	printf("%d\n", pop(&s));

	printf("%d\n", peek(&s));
	return 0;
}
```

주의 해야 할 점이 있다.

push() 함수에서 item을 넣어 줄 때 s->data[++(s->top)] 로 top을 1 증가시킨 후에 item을 넣어줘야 한다.

pop() 함수에서 item을 반환할 때 s->data[(s->top)--]로 top에 있는 요소를 반환한 후에 1 감소시켜줘야 한다.

추후에 나올 내용으로 Queue에서는 pop() (dequeue())을 할 때 q->data[++(q->front)]로 front를 1 증가시킨 후에 요소를 반환해야 한다.



**스택의 요소를 구조체로**

```c
#include <stdio.h>
#include <stdlib.h>
#define MAX_STACK_SIZE 100
#define MAX_STRING 100

typedef struct {
    int student_no;
    char name[MAX_STRING];
    char address[MAX_STRING];
}element;

typedef struct {
	element data[MAX_STACK_SIZE];
	int top;
}StackType;
```

여기서 top과 stack 배열을 하나의 구조체로 결합시키고 이 구조체의 포인터를 함수로 전달하여 여러 개의 스택을 동시에 사용할 수 있다.



**스택 동적 메모리 할당**

```c
int main(void) {
	StackType *s;
	s = (StackType *)malloc(sizeof(StackType));

	init_stack(&s);
	
	push(s, 1);
	push(s, 4);
	push(s, 2);
	push(s, 6);
	push(s, 9);
	push(s, 4);
	push(s, 7);


	printf("%d\n", pop(s));
	printf("%d\n", pop(s));
	printf("%d\n", peek(s));
	printf("%d\n", pop(s));
	printf("%d\n", peek(s));
    
	free(s.data);
	return 0;
}
```



### 동적 배열 스택

```c
#include <stdio.h>
#include <stdlib.h>
#define MAX_STACK_SIZE 100

typedef int element;

//동적 배열
typedef struct {
	element* data;
	int capacity;
	int top;
}StackType;

//intialization
void init_stack(StackType* s) {
	s->top = -1;
	s->capacity = 1;
	s->data = (element*)malloc(s->capacity * sizeof(element));
}

//delete stack
void delete1(StackType* s) {
	free(s);
}

//is_full
int is_full(StackType* s) {
	return (s->top == (s->capacity - 1));
}

//is_empty
int is_empty(StackType* s) {
	return (s->top == -1);
}

//push
//포화시 배열 2배 늘림
void push(StackType* s, element item) {
	if (is_full(s)) {
		s->capacity *= 2;
		s->data = (element*)realloc(s->data, s->capacity * sizeof(element));
	}
	s->data[++(s->top)] = item;
}

//pop
element pop(StackType* s) {
	if (is_empty(s)) {
		fprintf(stderr, "공백상태\n");
		exit(1);
	}
	else {
		return s->data[(s->top)--];
	}
}

//peek
element peek(StackType* s) {
	if (is_empty(s)) {
		fprintf(stderr, "공백상태\n");
		exit(1);
	}
	else {
		return s->data[s->top];
	}
}

int main(void) {
	StackType *s;
	s = (StackType *)malloc(sizeof(StackType));

	init_stack(&s);
	
	push(s, 1);
	push(s, 4);
	push(s, 2);
	push(s, 6);
	push(s, 9);
	push(s, 4);
	push(s, 7);


	printf("%d\n", pop(s));
	printf("%d\n", pop(s));
	printf("%d\n", peek(s));
	printf("%d\n", pop(s));
	printf("%d\n", peek(s));
    
	free(s.data);
	return 0;
}  
```



## 스택의 응용: 괄호 검사

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#define MAX_STACK_SIZE 100

typedef char element;

typedef struct {
	element data[MAX_STACK_SIZE];
	int top;
}StackType;

//init_stack
void init_stack(StackType* s) {
	s->top = -1;
}

//is_full
int is_full(StackType* s) {
	return (s->top == MAX_STACK_SIZE - 1);
}

//is_empty
int is_empty(StackType* s) {
	return (s->top == -1);
}

//push
void push(StackType* s, element item) {
	if (is_full(s)) {
		fprintf(stderr, "포화상태\n");
	}	
	s->data[++(s->top)] = item;
}

//pop
char pop(StackType* s) {
	if (is_empty(s)) {
		fprintf(stderr, "공백상태\n");
		exit(1);
	}
	else {
		return s->data[(s->top)--];
	}
}

//peek
char peek(StackType* s) {
	if (is_empty(s)) {
		fprintf(stderr, "공백상태\n");
		exit(1);
	}
	else {
		return s->data[s->top];
	}
}

int check(const char* in) {
	StackType s;
	char ch, open_ch;
	int i, n = strlen(in);
	init_stack(&s);
	
	for (i = 0; i < n; i++) {
		ch = in[i];
		switch (ch) {
		case '(': case '{': case '[':
			push(&s, ch);
			break;
		case ')': case '}': case ']':
			if (is_empty(&s)) {
				return 0;
			}
			else {
				open_ch = pop(&s);
				if ((open_ch == '(' && ch != ')') || (open_ch == '{' && ch != '}') || (open_ch == '[' && ch != ']')){
					return 0;
				}
				break;
			}
		}
	}
	if (!is_empty(&s)) {
		return 0;
	}
	else {
		return 1;
	}
}

int main(void) {
	char* p = "{A[(i+1)]=0;}";
	if (check(p) == 1) {
		printf("%s 성공", p);
	}
	else {
		printf("%s 실패", p);
	}
	return 0;
}
```



## 스택의 응용: 후위 표기 수식의 계산

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#define MAX_STACK_SIZE 100

typedef char element;

typedef struct {
	element data[MAX_STACK_SIZE];
	int top;
}StackType;

//init_stack
void init_stack(StackType* s) {
	s->top = -1;
}

//is_full
int is_full(StackType* s) {
	return (s->top == MAX_STACK_SIZE - 1);
}

//is_empty
int is_empty(StackType* s) {
	return (s->top == -1);
}

//push
void push(StackType* s, element item) {
	if (is_full(s)) {
		fprintf(stderr, "포화상태\n");
	}
	s->data[++(s->top)] = item;
}

//pop
element pop(StackType* s) {
	if (is_empty(s)) {
		fprintf(stderr, "공백상태\n");
		exit(1);
	}
	else {
		return s->data[(s->top)--];
	}
}

//peak
element peek(StackType* s) {
	if (is_empty(s)) {
		fprintf(stderr, "공백상태\n");
		exit(1);
	}
	else {
		return s->data[s->top];
	}
}

//우선 순위 검사
int prec(char op) {
	switch (op) {
	case '(': case ')':
		return 0;
	case '+': case '-':
		return 1;
	case '*': case '/':
		return 2;
	}
	return -1;
}

//중위 표기 -> 후위 표기
void InfixToPostfix(char exp[]) {
	int i = 0;
	char ch, top_op;
	char temp[MAX_STACK_SIZE];
	int result, k = 0;
	int len = strlen(exp);
	StackType s;

	init_stack(&s);
	for (i = 0; i < len; i++) {
		ch = exp[i];
		switch (ch) {
		case '+': case '-': case '*': case '/':
			while (!is_empty(&s) && (prec(ch) <= prec(peek(&s)))) {
				printf("%c", temp[k++] = pop(&s));
			}
			push(&s, ch);
			break;
		case '(':
			push(&s, ch);
			break;
		case ')':
			top_op = pop(&s);
			while (top_op != '(') {
				printf("%c", temp[k++]=top_op);
				top_op  = pop(&s);
			}
			break;
		default:
			printf("%c", temp[k++] = ch);
			break;
		}
	}
	while (!is_empty(&s)) {
		printf("%c", temp[k++]=pop(&s));
		printf("%d ", k);
	}
	printf("\n");
	printf("결과값: ");
	printf("%d", eval(temp, k));
	
}

int eval(char exp[], int length) {
	int op1, op2, value, i = 0;
	//int len = strlen(exp);
	int len = length;
	char ch;
	StackType t;

	init_stack(&t);
	for (i = 0; i < len; i++) {
		ch = exp[i];
		if (ch != '+' && ch != '-' && ch != '*' && ch != '/') {
			value = ch - '0';
			push(&t, value);
		}
		else {
			op2 = pop(&t);
			op1 = pop(&t);

			switch (ch) {
			case '+':
				push(&t, op1 + op2);
				break;
			case '-':
				push(&t, op1 - op2);
				break;
			case '*':
				push(&t, op1 * op2);
				break;
			case '/':
				push(&t, op1 / op2);
				break;
			}
		}
	}
	return pop(&t);
}

int main(void) {

	char* s = "(2+3)*4+9";
	printf("중위표기식: %s\n", s);
	printf("후위표기식: ");
	InfixToPostfix(s);
	printf("\n");

	return 0;
}
```



## 스택의 응용: 미로 게임

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#define MAZE_SIZE 6
#define MAX_STACK_SIZE 100



typedef struct {
	short r;
	short c;
} element;

typedef struct {
	element data[MAX_STACK_SIZE];
	int top;
} StackType;

//스택 초기화 함수
void init_stack(StackType *s) {
	s->top = -1;
}
//공백 상태 검출 함수
int is_empty(StackType* s) {
	return(s->top == -1);
}

//포화 상태 검출 함수
int is_full(StackType* s) {
	return (s->top == (MAX_STACK_SIZE - 1));
}

//삽입 함수
void push(StackType* s, element item) {
	if (is_full(s)) {
		fprintf(stderr, "스택 포화 에러\n");
		return;
	}
	else s->data[++(s->top)] = item;
}

//삭제 함수
element pop(StackType* s) {
	if (is_empty(s)) {
		fprintf(stderr, "스택 공백 에러\n");
		exit(1);
	}
	else return s->data[(s->top)--];
}

//피크 함수
element peek(StackType* s) {
	if (is_empty(s)) {
		fprintf(stderr, "스택 공백 에러\n");
		exit(1);
	}
	else return s->data[s->top];
}

element here = { 1,0 }, entry = { 1,0 };

char maze[MAZE_SIZE][MAZE_SIZE] = {
	{'1','1','1','1','1','1'},
	{'e','0','1','0','0','1'},
	{'1','0','0','0','1','1'},
	{'1','0','1','0','1','1'},
	{'1','0','1','0','0','x'},
	{'1','1','1','1','1','1'}
};

void push_loc(StackType* s, int r, int c) {
	if (r < 0 || c < 0) return;
	if (maze[r][c] != '1' && maze[r][c] != '.') {
		element tmp = { 0,0 };
		tmp.r = r;
		tmp.c = c;
		push(s, tmp);
	}
}

void maze_print(char maze[MAZE_SIZE][MAZE_SIZE]) {
	printf("\n");
	for (int r = 0; r < MAZE_SIZE; r++) {
		for (int c = 0; c < MAZE_SIZE; c++) {
			printf("%c", maze[r][c]);
		}
		printf("\n");
	}
}

int main(void) {
	int r, c;
	StackType s;

	init_stack(&s);
	here = entry;
	while (maze[here.r][here.c] != 'x') {
		r = here.r;
		c = here.c;
		maze[r][c] = '.';
		maze_print(maze);
		push_loc(&s, r - 1, c);
		push_loc(&s, r + 1, c);
		push_loc(&s, r, c - 1);
		push_loc(&s, r, c + 1);

		if (is_empty(&s)) {
			printf("실패\n");
			return;
		}
		else
			here = pop(&s);
	}
	printf("성공\n");
	return 0;
}
```

