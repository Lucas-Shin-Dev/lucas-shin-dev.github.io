---
layout: single
title:  "Chapter 6. 연결 리스트 (1)"
categories: DataStructure
tag: [자료구조, C언어, 나작복]
toc: true
author_profile: false
sidebar:
    nav: "docs"
search: true #true, false
use_math: true
---



## List (리스트)

리스트의 항목들은 순서 또는 위치를 가진다.

스택과 큐도 넓게 보면 리스트의 일종이다.



### 리스트 ADT

```
객체: n개의 element형으로 구성된 순서 있는 모임
연산:
	insert(list, pos, item) ::= pos 위치에 요소를 추가한다.
	insert_last(list, item) ::= 맨 끝에 요소를 추가한다.
	insert_firtst(list, item) ::= 맨 처음에 요소를 추가한다.
	delete(list, pos) ::= pos 위치의 요소를 제거한다.
	clear(list) ::= 리스트의 모든 요소를 제거한다.
	get_entry(list, pos) ::= pos 위치의 요소를 반환한다.
	get_length(list) ::= 리스트의 길이를 구한다.
	is_empty(list) ::= 리스트가 비어있는지를 검사한다.
	is_full(list) ::= 리스트가 꽉 찼는지를 검사한다.
	print_list(list) ::= 리스트의 모든 요소를 표시한다.
```

리스트는 **배열**과 **연결 리스트**를 이용하여 구현할 수 있다.

배열을 이용하면 쉽게 구현 가능하며 속도가 빠르다는 장점이 있다.

반면에 크기가 고정되고 리스트 중간에 삽입 삭제를 하기 위해서는 기존의 데이터들을 이동해야 하는 단점이 있다.



다른 방법으로는 포인터를 이용하여 연결 리스트를 만드는 것이다.

연결 리스트는 크기가 제한되지 않고, 중간에서 쉽게 삽입 삭제를 할 수 있게 구현할 수 있다.

그러나 구현이 복잡하고 임의의 항목을 추출하려고 할 때는 배열을 사용하는 방법보다 시간이 오래 걸린다.



### 배열로 구현된 리스트 구현

```c
#include <stdio.h>
#define MAX_LIST_SIZE 100

typedef int element;

typedef struct {
	element array[MAX_LIST_SIZE];
	int size;
}ArrayListType;

//error
void error(char* message) {
	fprintf(stderr, "%s\n", message);
	exit(1);
}

//init
void init(ArrayListType* L) {
	L->size = 0;
}

int is_empty(ArrayListType* L) {
	return L->size == 0;
}

int is_full(ArrayListType* L) {
	return L->size == MAX_LIST_SIZE;
}

element get_entry(ArrayListType* L, int pos) {	//위치 필요
	if (pos < 0 || pos >= L->size) {
		error("위치 오류");
	}
	else {
		return L->array[pos];
	}
}

void print_list(ArrayListType* L) {
	for (int i = 0; i < L->size; i++) {
		printf("%d ->", L->array[i]);
	}
	printf("\n");
}

//뒤에 삽입
void insert_last(ArrayListType* L, element item) {
	if (L->size >= MAX_LIST_SIZE) {
		error("리스트 오버플로우");
	}
	else {
		L->array[L->size++] = item;
	}
}

//중간에 삽입
void insert(ArrayListType* L, int pos, element item) {	////위치 필요	0이면 맨앞
	if (!is_full(L) && (pos >= 0) && (pos <= L->size)) {
		for (int i = (L->size - 1); i >= pos; i--) {	//한칸씩 뒤로 미루기
			L->array[i + 1] = L->array[i];
		}
		L->array[pos] = item;	//삽입하려는 위치에 저장
		L->size++;	//size 증가
	}
}

//삭제
element delete(ArrayListType* L, int pos) {	////위치 필요
	element item;

	if (pos < 0 || pos >= L->size) {
		error("위치 오류");
	}
	else {
		item = L->array[pos];
		for (int i = pos; i < (L->size - 1); i++) {
			L->array[i] = L->array[i + 1];
		}
		L->size--;

		return item;
	}
}

int main(void) {
	ArrayListType list;

	init(&list);

	insert(&list, 0, 10);
	print_list(&list);
	
	insert(&list, 0, 20);
	print_list(&list);
	
	insert(&list, 1, 30);
	print_list(&list);

	insert_last(&list, 40);
	print_list(&list);

	delete(&list, 0);
	print_list(&list);
	return 0;
}
```



### 연결 리스트

연결 리스트는 노드(node)들의 집합이다.

노드는 **데이터 필드(data field)**와 **링크 필드(link field)**로 구성되어 있다.

데이터 필드에는 저장하려는 데이터가 들어 있다.

링크 필드에는 다음 노드를 가리키는 포인터가 저장된다.

이 포인터를 이용해 다음 노드로 이동할 수 있는 것이다.

마지막 노드의 링크 필드는 **NULL**로 설정하여 더 이상 연결된 노드가 없다는 것을 표시한다.

그리고 첫 번째 노드를 가리키고 있는 변수 **헤드 포인터(head pointer)**가 필수적으로 필요하다.



![image-20230408180954010]({{site.url}}\images\2023-04-08-Review0408-DataStructure\image-20230408180954010.png)

(+ 이중 원형 연결 리스트)



## 단순 연결 리스트

### 삽입 연산

맨 앞에 삽입하는 경우

![image-20230408181129030]({{site.url}}\images\2023-04-08-Review0408-DataStructure\image-20230408181129030.png)

(1) 추가할 노드p 생성

(2) 노드p의 데이터 필드에 데이터 저장

(3) 노드p의 링크 필드에 head가 가리키는 노드의 주소를 저장

(4) head에 노드p의 주소를 저장



중간(노드 pre 뒤)에 삽입하는 경우

![image-20230408181511394]({{site.url}}\images\2023-04-08-Review0408-DataStructure\image-20230408181511394.png)

(1) 추가할 노드 p 생성

(2) 노드p의 데이터 필드에 데이터 저장

(3) 노드p의 링크 필드에 노드pre의 링크 필드에 저장된 값(기존 pre 다음 노드의 주소)을 저장

(4) 노드pre의 링크 필드에 새로 추가할 노드p의 주소를 저장



### 삭제 연산

맨 앞을 삭제하는 경우

![image-20230408181917752]({{site.url}}\images\2023-04-08-Review0408-DataStructure\image-20230408181917752.png)

(1) 노드r에 첫 번째 노드의 주소를 저장(head)

(2) head에 첫 번째 노드의 링크 필드에 있는 값(두 번째 노드의 주소)을 저장

(3) 첫 번째 노드 삭제



중간(노드 pre 뒤)에 삭제하는 경우

![image-20230408182102665]({{site.url}}\images\2023-04-08-Review0408-DataStructure\image-20230408182102665.png)

(1) 노드r에 삭제하려는 노드 p의 주소를 저장

(2) 노드 pre의 링크 필드에 노드p의 링크 필드에 저장된 값(노드p 다음 노드의 주소)을 저장

(3) 노드p 삭제



### 연결 리스트 구현

```c
#include <stdio.h>

typedef int element;

typedef struct ListNode{
	element data;	//data field
	struct ListNode* link;	//link field
}ListNode;

ListNode* insert_first(ListNode* head, int value) {
	ListNode* p = (ListNode*)malloc(sizeof(ListNode));	//노드p 생성
	p->data = value;
	p->link = head;
	head = p;

	return head;
}

ListNode* insert(ListNode* head, ListNode* pre, int value) {	//head 노드 필수
	ListNode* p = (ListNode*)malloc(sizeof(ListNode));	//노드p 생성
	p->data = value;
	p->link = pre->link;
	pre->link = p;
	
	return head;
}

ListNode* delete_first(ListNode* head) {
	ListNode* removed;
	if (head == NULL) {
		return NULL;
	}
	else {
		removed = head;	//removed에 head에 저장된 주소를 넣음
		head = removed->link;	//head에 removed가 가리키는 주소의 link가 가리키는 주소를 넣음(첫번째 노드의 link는 두번째 노드의 주소를 가리키고 있음)
		free(removed);	//removed 반납

		return head;
	}
}

ListNode* delete(ListNode* head, ListNode* pre) {
	ListNode* removed;
	if (head == NULL) {
		return NULL;
	}
	else {
		removed = pre->link;
		pre->link = removed->link;
		free(removed);

		return head;
	}
}

void print_list(ListNode* head) {
	for (ListNode* p = head; p != NULL; p = p->link) {
		printf("%d->", p->data);
	}
	printf("NULL\n");
}

int main(void) {
	ListNode* head = NULL;

	for (int i = 0; i < 5; i++) {
		head = insert_first(head, i);
		print_list(head);
	}
	for (int i = 0; i < 5; i++) {
		head = delete_first(head);
		print_list(head);
	}
	return 0;
}
```



### 추가

```c
#include <stdio.h>

typedef int element;

typedef struct ListNode {
	element data;	//data field
	struct ListNode* link;	//link field
}ListNode;

ListNode* insert_first(ListNode* head, int value) {
	ListNode* p = (ListNode*)malloc(sizeof(ListNode));	//노드p 생성
	p->data = value;
	p->link = head;
	head = p;

	return head;
}

ListNode* insert(ListNode* head, ListNode* pre, int value) {	//head 노드 필수
	ListNode* p = (ListNode*)malloc(sizeof(ListNode));	//노드p 생성
	p->data = value;
	p->link = pre->link;
	pre->link = p;

	return head;
}

ListNode* delete_first(ListNode* head) {
	ListNode* removed;
	if (head == NULL) {
		return NULL;
	}
	else {
		removed = head;	//removed에 head에 저장된 주소를 넣음
		head = removed->link;	//head에 removed가 가리키는 주소의 link가 가리키는 주소를 넣음(첫번째 노드의 link는 두번째 노드의 주소를 가리키고 있음)
		free(removed);	//removed 반납

		return head;
	}
}

ListNode* delete(ListNode* head, ListNode* pre) {
	ListNode* removed;
	if (head == NULL) {
		return NULL;
	}
	else {
		removed = pre->link;
		pre->link = removed->link;
		free(removed);

		return head;
	}
}

void print_list(ListNode* head) {
	for (ListNode* p = head; p != NULL; p = p->link) {
		printf("%d->", p->data);
	}
	printf("NULL\n");
}

//검색
ListNode* search_list(ListNode* head, element x) {
	ListNode* p = head;

	while (p != NULL) {
		if (p->data == x) {
			return p;
		}
		else {
			p = p->link;
		}
	}
	return NULL;	//탐색 실패
}

//역
ListNode* reverse(ListNode* head) {
	ListNode* p, * q, * r;
	p = head;
	q = NULL;
	
	while (p != NULL) {
		r = q;	//r에 q의 값
		q = p;	//q에 p(head)(첫번째 노드) 주소
		p = p->link;	//p에 첫번째 노드의 link가 가리키는 두번째 노드 주소
		q->link = r;	//q의 link에 q의 주소
	}
	return q;
}

//병합
ListNode* concat_list(ListNode* head1, ListNode* head2) {
	if (head1 == NULL) {
		return head2;
	}
	else if (head2 == NULL) {
		return head1;
	}
	else {
		ListNode* p;
		p = head1;
		while (p != NULL) {
			p = p->link;
		}
		p->link = head2;
		return head1;
	}
}

int main(void) {
	ListNode* head1 = NULL;
	ListNode* head2 = NULL;

	head1 = insert_first(head1, 10);
	head1 = insert_first(head1, 20);
	head1 = insert_first(head1, 30);
	print_list(head1);

	head2 = reverse(head1);
	print_list(head2);

	return 0;
}
```



## 연결 리스트의 응용: 다항식

```c
#include <stdio.h>

typedef int element;

//노드 타입
typedef struct ListNode {
	int coef;	//계수
	int expon;	//차수
	struct ListNode* link;	//link field
}ListNode;

//연결 리스트 헤더
typedef struct ListType {
	int size;
	ListNode* head;
	ListNode* tail;
}ListType;

void error(char* message) {
	fprintf(stderr, "%s\n", message);
	exit(1);
}

//리스트 헤더 생성
ListType* create() {
	ListType* plist = (ListType*)malloc(sizeof(ListType));
	plist->size = 0;
	plist->head = plist->tail = NULL;

	return plist;
}

void insert_last(ListType* plist, int coef, int expon) {
	ListNode* temp = (ListNode*)malloc(sizeof(ListNode));

	if (temp == NULL) {
		error("메모리 할당 에러");
	}
	else {
		temp->coef = coef;
		temp->expon = expon;
		temp->link = NULL;	//마지막 노드여서 NULL

		if (plist->tail == NULL) {	//마지막 식
			plist->head = plist->tail = temp;
		}
		else {	//뒤에 식이 더 있음
			plist->tail->link = temp;
			plist->tail = temp;
		}
	}
}

void poly_add(ListType* plist1, ListType* plist2, ListType* plist3) {
	ListNode* a = plist1->head;
	ListNode* b = plist2->head;
	int sum;

	while (a && b) {	//a랑 b가 있으면
		if (a->expon == b->expon) {	//a,b 차수 같으면 둘의 계수를 더함
			sum = a->coef + b->coef;
			if (sum != 0) insert_last(plist3, sum, a->expon);	//0이면 plist3에 저장, 0이면 저장 안함
			a = a->link;	//두번째 노드
			b = b->link;	//두번째 노드
		}
		else if (a->expon > b->expon) {	//a의 차수가 더 크면 a의 계수를 plist3에 저장
			insert_last(plist3, a->coef, a->expon);
			a = a->link;
		}
		else {	//b의 차수가 더 크면 b의 계수를 plist3에 저장
			insert_last(plist3, b->coef, b->expon);
			b = b->link;
		}
	}
	for (; a != NULL; a = a->link) {	//b는 NULL이면 남은 a를 모두 저장
		insert_last(plist3, a->coef, a->expon);
	}
	for (; b != NULL; b = b->link) {	//a는 NULL이면 남은 b를 모두 저장
		insert_last(plist3, b->coef, b->expon);
	}
}

void poly_print(ListType* plist) {
	ListNode* p = plist->head;

	printf("polynomial = ");
	for (; p; p = p->link) {
		printf("%d^%d + ", p->coef, p->expon);
	}
	printf("\n");
}

int main(void) {
	ListType* list1, * list2, * list3;

	list1 = create();
	list2 = create();
	list3 = create();

	insert_last(list1, 3, 12);
	insert_last(list1, 2, 8);
	insert_last(list1, 1, 0);

	insert_last(list2, 8, 12);
	insert_last(list2, -3, 10);
	insert_last(list2, 10, 6);

	poly_print(list1);
	poly_print(list2);

	poly_add(list1, list2, list3);
	poly_print(list3);

	free(list1);
	free(list2);
	free(list3);

}
```

