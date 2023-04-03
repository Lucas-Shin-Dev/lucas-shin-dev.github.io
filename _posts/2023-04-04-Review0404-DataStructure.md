---
layout: single
title:  "Chapter 5. 큐"
categories: DataStructure
tag: [자료구조, C언어, 나작복]
toc: true
author_profile: false
sidebar:
    nav: "docs"
search: true #true, false
use_math: true
---



## Queue (큐)

선입선출(FIFO: First In First Out)로 먼저 들어온 데이터가 가장 먼저 나간다.

스택과 마찬가지로 중간에서 데이터를 삭제할 수 없다.

스택의 경우, 삽입과 삭제가 같은 쪽에서 일어나지만 큐에서는 삽입과 삭제가 다른 쪽에서 일어난다.

큐의 삽입이 일어나는 곳을 후단(rear), 삭제가 일어나는 곳을 전단(front)라고 한다.



### 큐 ADT

```
객체: 0개 이상의 요소들로 구성된 선형 리스트
연산:
	create(max_size) ::= 최대 크기가 max_size인 공백큐를 생성한다.
	init(q) ::= 큐를 초기화한다.
	is_empty(q) ::=
		if(size == 0) return TRUE;
		else return FALSE;
	enqueue(q, e) ::=
		if(is_full(q)) queue_full 오류;
		else q의 끝에 e를 추가한다.
	dequeue(q) ::=
		if(is_empty(q)) queue_empty 오류;
		else q의 맨 앞에 있는 e를 제거하여 반환한다.
	peek(q) ::=
		if(is_empty(q)) queue_empty 오류;
		else q의 맨 앞에 있는 e를 읽어서 반환한다.
```



### 선형큐 구현

```c
#include <stdio.h>
#include <stdlib.h>
#define MAX_QUEUE_SIZE 5
//create, init, in_empty, is_full, enqueue, dequeue, peek +error, print

typedef int element;

//create Queue struct
typedef struct {
	int front;
	int rear;
	element data[MAX_QUEUE_SIZE];
}QueueType;

//error function
void error(char* message) {
	fprintf(stderr, "%s\n", message);
	exit(1);
}

//init Queue
void init_queue(QueueType* q) {
	q->front = -1;
	q->rear = -1;
}

//print
void queue_print(QueueType* q) {
	for (int i = 0; i < MAX_QUEUE_SIZE; i++) {
		if (i <= q->front || i > q->rear) {	//front보다 작거나 rear보다 크면 비어있는걸로
			printf(" |");
		}
		else {
			printf("%d |", q->data[i]);
		}
	}
	printf("\n");
}

//is_full
int is_full(QueueType* q) {
	if (q -> rear == MAX_QUEUE_SIZE - 1) {
		return 1;
	}
	else {
		return 0;
	}
}

//is_empty
int is_empty(QueueType* q) {
	if (q->front == q->rear) {
		return 1;
	}
	else {
		return 0;
	}
}

//enqueue
void enqueue(QueueType* q, int item) {
	if (is_full(q)) {
		error("포화상태");
		return;
	}
	else {
		q->data[++(q->rear)] = item;
	}
}

//dequeue
int dequeue(QueueType* q) {
	if (is_empty(q)) {
		error("공백상태");
		return -1;
	}
	else {
		return q->data[++(q->front)];	//******************************************중요
	}
}

//peek
int peek(QueueType* q) {
	if (is_empty(q)) {
		error("공백상태");
		return -1;
	}
	else {
		return q->data[q->front];
	}
}

int main(void) {
	int item = 0;
	QueueType q;

	init_queue(&q);

	enqueue(&q, 10);
	queue_print(&q);

	enqueue(&q, 20);
	queue_print(&q);

	enqueue(&q, 30);
	queue_print(&q);

	item = dequeue(&q);
	queue_print(&q);
	
	item = dequeue(&q);
	queue_print(&q);

	item = dequeue(&q);
	queue_print(&q);
	
	return 0;
}
```

선형큐의 front와 rear의 초기값은 -1이다.

front는 맨 앞의 데이터가 있는 위치 앞을 가리키며 rear는 맨 마지막의 데이터가 있는 위치를 가리킨다.

![image-20230403170148967]({{site.url}}\images\2023-04-04-Review0404-DataStructure\image-20230403170148967.png)

데이터가 입력되면 rear을 1 증가시키고 그 위치에 데이터를 저정한다.

삭제할 때도 front를 1 증가시키고 그 위치의 데이터를 삭제한다.



### 원형큐의 구현

선형큐는 front와 rear가 증가하기만 하기 때문에 언젠가 배열의 끝에 도달하게 되고 배열 앞부분이 비어있더라도 사용하지 못한다는 단점이 있다.

이를 보완한게 원형큐이다.

front와 rear의 값이 배열의 끝인 (MAX_QUEUE_SIZE - 1)에 도달하면 다음에 증가되는 값은 0이 되도록 하는 것이다

즉 배열이 원형으로 처음과 끝이 연결되어 있다고 생각하는 것이다.

물론 실제 배열이 원형으로 변화되는 것이 아니라 개념상 원형으로 배열 인덱스를 변화시켜주는 것 뿐이다.

```c
#include <stdio.h>
#include <stdlib.h>
#define MAX_QUEUE_SIZE 5
//create, init, in_empty, is_full, enqueue, dequeue, peek +error, print
//front, rear 나머지를 이용해서 원형 큐

typedef int element;

//create Queue struct
typedef struct {
	int front;
	int rear;
	element data[MAX_QUEUE_SIZE];
}QueueType;

//error function
void error(char* message) {
	fprintf(stderr, "%s\n", message);
	exit(1);
}

//init Queue
void init_queue(QueueType* q) {
	q->front = 0;	//선형과 달리 원형은 front, rear 0
	q->rear = 0;
}

//print
void queue_print(QueueType* q) {
	printf("QUEUE(front=%d rear=%d) = ", q->front, q->rear);
	if (!is_empty(q)) {
		int i = q->front;
		do {
			i = (i + 1) % (MAX_QUEUE_SIZE);
			printf("%d | ", q->data[i]);
			if (i == q->rear) {
				break;
			}
		} while (i != q->front);
	}
	printf("\n");
}

//is_full
int is_full(QueueType* q) {
	if ((q->rear + 1) % MAX_QUEUE_SIZE == q->front) {	//rear+1 에 MAX_STACK_SIZE 나눈 나머지가 front와 같으면 포화
		return 1;
	}
	else {
		return 0;
	}
}

//is_empty
int is_empty(QueueType* q) {
	if (q->front == q->rear) {	//선형과 동일하게 둘이 같으면 공백
		return 1;
	}
	else {
		return 0;
	}
}

//enqueue
void enqueue(QueueType* q, int item) {
	if (is_full(q)) {
		error("포화상태");
		return;
	}
	else {
		q->rear = (q->rear + 1) % MAX_QUEUE_SIZE;	//rear 1 증가 시킴
		q->data[q->rear] = item;	//앞에서 1 증가 시켰기 때문에 또 증가시키면 안됨
	}
}

//dequeue
int dequeue(QueueType* q) {
	if (is_empty(q)) {
		error("공백상태");
		return -1;
	}
	else {
		q->front = (q->front + 1) % MAX_QUEUE_SIZE;
		return q->data[q->front];	//**********************************중요
	}
}

//peek
int peek(QueueType* q) {
	if (is_empty(q)) {
		error("공백상태");
		return -1;
	}
	else {
		q->front = (q->front+1) % MAX_QUEUE_SIZE;
		return q->data[(q->front)--];
	}
}

int main(void) {
	int item = 0;
	QueueType q;

	init_queue(&q);

	enqueue(&q, 10);
	queue_print(&q);

	enqueue(&q, 20);
	queue_print(&q);

	enqueue(&q, 30);
	queue_print(&q);

	item = dequeue(&q);
	queue_print(&q);

	item = peek(&q);
	queue_print(&q);

	item = dequeue(&q);
	queue_print(&q);

	return 0;
}
```

원형큐는 선형큐와 달리 front와 rear의 초기값이 -1이 아닌 0이다.

또 front는 항상 큐의 첫 번째 요소의 하나 앞을, rear는 마지막 요소를 가리킨다.

![image-20230403170727670]({{site.url}}\images\2023-04-04-Review0404-DataStructure\image-20230403170727670.png)

front와 rear의 값이 같으면 원형큐가 비어 있음을 나타낸다.

그리고 원형큐에서는 하나의 자리는 항상 비워둔다.

왜냐하면 포화 상태와 공백 상태를 구별하기 위해서이다.

따라서 front와 rear의 값이 같으면 공백 상태, front가 rear보다 하나 앞에 있으면 포화 상태가 된다.

+추가적인 변수를 사용하면 한자리를 비워두지 않아도 된다.



원형큐에서 요소를 삽입할 때 rear에 1을 증가시킨 후 MAX_QUEUE_SIZE로 나머지 연산을 하여 마지막 인덱스를 넘어가도 오류가 발생하지 않게 한다.

마찬가지로 요소를 삭제할 때 front에 1을 증가시킨 후 MAX_QUEUE_SIZE로 나머지 연산을 하여 마지막 인덱스를 넘어가도 오류가 발생하지 않게 한다.



## Deque (덱)

Deque은 double-ended queue의 줄임말로 큐의 front와 rear에서 모두 삽입과 삭제가 가능한 큐를 의미한다.

물론 중간에서 삽입하거나 삭제하는 것은 불가능하다.



### 덱 ADT

```
객체: n개의 element형의 요소들의 순서 있는 모임
연산:
	create() ::= 덱을 생성한다.
	inif(dq) ::= 덱을 초기화한다.
	is_empty(dq) ::= 덱이 공백 상태인지를 검사한다.
	is_full(dq) ::= 덱이 포화 상태인지를 검사한다.
	add_front(dq, e) ::= 덱의 앞에 요소를 추가한다.
	add_rear(dq, e) ::= 덱의 뒤에 요소를 추가한다.
	delete_front(dq) ::= 덱의 앞에 있는 요소를 반환한 다음 삭제한다.
	delete_rear(dq) ::= 덱의 뒤에 있는 요소를 반환한 다음 삭제한다.
	get_front(q) ::= 덱의 앞에서 삭제하지 않고 앞에 있는 요소를 반환한다.
	get_rear(q) ::= 덱의 뒤에서 삭제하지 않고 앞에 있는 요소를 반환한다.
```



### 덱의 구현

```c
#include <stdio.h>
#include <stdlib.h>
#define MAX_QUEUE_SIZE 5
//create, init, in_empty, is_full, enqueue, dequeue, peek +error, print
//front, rear 나머지를 이용해서 원형 큐
//front enqueue, rear dequeue, rear peek

typedef int element;

//create Queue struct
typedef struct {
	int front;
	int rear;
	element data[MAX_QUEUE_SIZE];
}QueueType;

//error function
void error(char* message) {
	fprintf(stderr, "%s\n", message);
	exit(1);
}

//init Queue
void init_queue(QueueType* q) {
	q->front = 0;	//선형과 달리 원형은 front, rear 0
	q->rear = 0;
}

//print
void queue_print(QueueType* q) {
	printf("QUEUE(front=%d rear=%d) = ", q->front, q->rear);
	if (!is_empty(q)) {
		int i = q->front;
		do {
			i = (i + 1) % (MAX_QUEUE_SIZE);
			printf("%d | ", q->data[i]);
			if (i == q->rear) {
				break;
			}
		} while (i != q->front);
	}
	printf("\n");
}

//is_full
int is_full(QueueType* q) {
	if ((q->rear + 1) % MAX_QUEUE_SIZE == q->front) {	//rear+1 에 MAX_STACK_SIZE 나눈 나머지가 front와 같으면 포화
		return 1;
	}
	else {
		return 0;
	}
}

//is_empty
int is_empty(QueueType* q) {
	if (q->front == q->rear) {	//선형과 동일하게 둘이 같으면 공백
		return 1;
	}
	else {
		return 0;
	}
}

//enqueue
void enqueue(QueueType* q, int item) {
	if (is_full(q)) {
		error("포화상태");
		return;
	}
	else {
		q->rear = (q->rear + 1) % MAX_QUEUE_SIZE;	//rear 1 증가 시킴
		q->data[q->rear] = item;	//앞에서 1 증가 시켰기 때문에 또 증가시키면 안됨
	}
}

//dequeue
int dequeue(QueueType* q) {
	if (is_empty(q)) {
		error("공백상태");
		return -1;
	}
	else {
		q->front = (q->front + 1) % MAX_QUEUE_SIZE;
		return q->data[q->front];	//*********************************중요
	}
}

//peek
int peek(QueueType* q) {
	if (is_empty(q)) {
		error("공백상태");
		return -1;
	}
	else {
		q->front = (q->front + 1) % MAX_QUEUE_SIZE;
		return q->data[(q->front)--];
	}
}
//============================================================
//front enqueue
void enqueue_front(QueueType* q, int item) {
	if (is_full(q)) {
		error("포화상태");
		return;
	}
	else {
		q->data[q->front] = item;
		q->front = (q->front - 1 + MAX_QUEUE_SIZE) % MAX_QUEUE_SIZE;	//MAX_QUEUE_SIZE를 더해줘서 음수가 되는 걸 방지
	}
}

//rear dequeue
int dequeue_rear(QueueType* q) {
	int pre = q->rear;
	if (is_empty(q)) {
		error("공백상태");
		return -1;
	}
	else {
		q->rear = (q->rear - 1 + MAX_QUEUE_SIZE) % MAX_QUEUE_SIZE;
		return q->data[pre];
	}
}

//rear peek
int peek_rear(QueueType* q) {
	if (is_empty(q)) {
		error("공백상태");
		return -1;
	}
	else {
		return q->data[q->rear];
	}
}

int main(void) {
	int item = 0;
	QueueType q;

	init_queue(&q);

	enqueue(&q, 10);
	queue_print(&q);

	enqueue(&q, 20);
	queue_print(&q);

	enqueue_front(&q, 30);
	queue_print(&q);

	enqueue(&q, 40);
	queue_print(&q);

	item = dequeue(&q);
	queue_print(&q);

	item = dequeue_rear(&q);
	queue_print(&q);

	item = dequeue_rear(&q);
	queue_print(&q);

	return 0;
}
```

덱은 요소를 front에 삽입할 때 현재 front에 요소를 삽입한 후 1을 감소시킨 후 MAX_QUEUE_SIZE를 더해준 값에 MAX_QUEUE_SIZE로 나머지 연산을 하여 구한다.

MAX_QUEUE_SIZE를 1번 더하는 이유는 front의 값이 음수가 되는 경우를 대비하기 위함이다.

마찬가지로 rear에서 삭제할 때 현재 rear에 있는 요소를 반환한 후 rear에 1을 감소시킨 후 MAX_QUEUE_SIZE를 더해준 값에 MAX_QUEUE_SIZE로 나머지 연산을 하여 구한다.

삽일할 때와 같은 이유로 rear의 값이 음수가 되는 경우를 대비하기 위함이다.



## 큐의 응용: 버퍼

```c
#include <stdio.h>
#include <stdlib.h>
#define MAX_QUEUE_SIZE 5
//create, init, in_empty, is_full, enqueue, dequeue, peek +error, print
//front, rear 나머지를 이용해서 원형 큐

typedef int element;

//create Queue struct
typedef struct {
	int front;
	int rear;
	element data[MAX_QUEUE_SIZE];
}QueueType;

//error function
void error(char* message) {
	fprintf(stderr, "%s\n", message);
	exit(1);
}

//init Queue
void init_queue(QueueType* q) {
	q->front = 0;	//선형과 달리 원형은 front, rear 0
	q->rear = 0;
}

//print
void queue_print(QueueType* q) {
	printf("QUEUE(front=%d rear=%d) = ", q->front, q->rear);
	if (!is_empty(q)) {
		int i = q->front;
		do {
			i = (i + 1) % (MAX_QUEUE_SIZE);
			printf("%d | ", q->data[i]);
			if (i == q->rear) {
				break;
			}
		} while (i != q->front);
	}
	printf("\n");
}

//is_full
int is_full(QueueType* q) {
	if ((q->rear + 1) % MAX_QUEUE_SIZE == q->front) {	//rear+1 에 MAX_STACK_SIZE 나눈 나머지가 front와 같으면 포화
		return 1;
	}
	else {
		return 0;
	}
}

//is_empty
int is_empty(QueueType* q) {
	if (q->front == q->rear) {	//선형과 동일하게 둘이 같으면 공백
		return 1;
	}
	else {
		return 0;
	}
}

//enqueue
void enqueue(QueueType* q, int item) {
	if (is_full(q)) {
		error("포화상태");
		return;
	}
	else {
		q->rear = (q->rear + 1) % MAX_QUEUE_SIZE;	//rear 1 증가 시킴
		q->data[q->rear] = item;	//앞에서 1 증가 시켰기 때문에 또 증가시키면 안됨
	}
}

//dequeue
int dequeue(QueueType* q) {
	if (is_empty(q)) {
		error("공백상태");
		return -1;
	}
	else {
		q->front = (q->front + 1) % MAX_QUEUE_SIZE;
		return q->data[q->front];	//******************************************중요
	}
}

//peek
int peek(QueueType* q) {
	if (is_empty(q)) {
		error("공백상태");
		return -1;
	}
	else {
		q->front = (q->front + 1) % MAX_QUEUE_SIZE;
		return q->data[(q->front)--];
	}
}

int main(void) {
	QueueType queue;
	int element;

	init_queue(&queue);
	srand(time(NULL));

	for (int i = 0; i < 100; i++) {
		if (rand() % 5 == 0) {
			enqueue(&queue, rand() % 100);
		}
		queue_print(&queue);
		if (rand() % 10 == 0) {
			int data = dequeue(&queue);
		}
		queue_print(&queue);
	}
	return 0;
}
```



## 큐의 응용: 시뮬레이션

```c
#include <stdio.h>
#include <stdlib.h>
#define MAX_QUEUE_SIZE 100
//create, init, in_empty, is_full, enqueue, dequeue, peek +error, print
//front, rear 나머지를 이용해서 원형 큐

typedef struct {
	int id;
	int arrival_time;
	int service_time;
}element;

//create Queue struct
typedef struct {
	int front;
	int rear;
	element data[MAX_QUEUE_SIZE];
}QueueType;

//error function
void error(char* message) {
	fprintf(stderr, "%s\n", message);
	exit(1);
}

//init Queue
void init_queue(QueueType* q) {
	q->front = 0;	//선형과 달리 원형은 front, rear 0
	q->rear = 0;
}

//print
void queue_print(QueueType* q) {
	printf("QUEUE(front=%d rear=%d) = ", q->front, q->rear);
	if (!is_empty(q)) {
		int i = q->front;
		do {
			i = (i + 1) % (MAX_QUEUE_SIZE);
			printf("%d | ", q->data[i]);
			if (i == q->rear) {
				break;
			}
		} while (i != q->front);
	}
	printf("\n");
}

//is_full
int is_full(QueueType* q) {
	if ((q->rear + 1) % MAX_QUEUE_SIZE == q->front) {	//rear+1 에 MAX_STACK_SIZE 나눈 나머지가 front와 같으면 포화
		return 1;
	}
	else {
		return 0;
	}
}

//is_empty
int is_empty(QueueType* q) {
	if (q->front == q->rear) {	//선형과 동일하게 둘이 같으면 공백
		return 1;
	}
	else {
		return 0;
	}
}

//enqueue
void enqueue(QueueType* q, element item) {
	if (is_full(q)) {
		error("포화상태");
		return;
	}
	else {
		q->rear = (q->rear + 1) % MAX_QUEUE_SIZE;	//rear 1 증가 시킴
		q->data[q->rear] = item;	//앞에서 1 증가 시켰기 때문에 또 증가시키면 안됨
	}
}

//dequeue
element dequeue(QueueType* q) {
	if (is_empty(q)) {
		error("공백상태");
		exit(1);
	}
	else {
		q->front = (q->front + 1) % MAX_QUEUE_SIZE;
		return q->data[q->front];	//******************************************중요
	}
}

//peek
element peek(QueueType* q) {
	if (is_empty(q)) {
		error("공백상태");
		exit(1);
	}
	else {
		q->front = (q->front + 1) % MAX_QUEUE_SIZE;
		return q->data[(q->front)--];
	}
}

int main(void) {
	int minutes = 60;
	int total_wait = 0;
	int total_customers = 0;
	int service_time = 0;
	int service_customer;
	QueueType q;

	init_queue(&q);

	srand(time(NULL));

	for (int clock = 0; clock < minutes; clock++) {
		printf("현재시각=%d\n", clock);
		if ((rand() % 10) < 3) {
			element customer;
			customer.id = total_customers++;
			customer.arrival_time = clock;
			customer.service_time = rand() % 3 + 1;
			enqueue(&q, customer);
			printf("고객 %d이 %d분에 들어옵니다. 업무처리시간= %d분\n",
				customer.id, customer.arrival_time, customer.service_time);
		}
		if (service_time > 0) {
			printf("고객 %d 업무처리중입니다. \n", service_customer);
			service_time--;
		}
		else {
			if (!is_empty(&q)) {
				element customer = dequeue(&q);
				service_customer = customer.id;
				service_time = customer.service_time;
				printf("고객 %d이 %d분에 업무를 시작합니다. 대기시간은 %d분이었습니다.\n", customer.id, clock, clock - customer.arrival_time);
				total_wait += clock - customer.arrival_time;
			}
		}
	}
	printf("전체 대기 시간=%d분 \n", total_wait);
	return 0;
}
```

