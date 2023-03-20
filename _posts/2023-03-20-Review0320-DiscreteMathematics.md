---
layout: single
title:  "Chapter 2. 논리와 명제"
categories: DiscreteMathematics
tag: [이산수학, 나작복]
toc: true
author_profile: false
sidebar:
    nav: "docs"
search: true #true, false
use_math: true
---

명제 논리: 주어와 술어를 구분하지 않고 전체를 하나의 식으로 처리하여 참과 거짓을 판별하는 법칙

술어 논리: 주어와 술어를 구분하여 참과 거짓에 관한 법칙



명제는 통상 영문 소문자로 표기한다.

참과 거짓 값을 가질 때 그 값을 명제의 진리값(truth value)라고 한다.



## 논리 연산

논리 연산자(Logical Operators)

​	단순 명제들을 연결시켜 주는 역할을 한다.

​	$\vee \$(논리합), $\wedge \$(논리곱), ~(부정)

![image-20230320135923042]({{site.url}}\images\2023-03-20-Review0320-DiscreteMathematics\image-20230320135923042.png)

논리 연산자를 포함하는 합성 명제에서 괄호가 없는 경우에는 다음과 같은 우선순위를 가진다.

~ $>\$ $\wedge \$ $>\$ $\vee \$ $>\$ $\rightarrow \$ $>\$ $\leftrightarrow\$

### NOT (부정, negation)

임의의 명제 p가 주어졌을 때 그 명제에 대한 NOT(부정)은 명제 p의 반대되는 진리값을 가진다.

~p 라고 표기하며 'not p 또는 p가 아니다' 라고 읽는다.

![image-20230320140129303]({{site.url}}\images\2023-03-20-Review0320-DiscreteMathematics\image-20230320140129303.png)



### AND (논리곱, conjunction)

임의의 두 명제 p, q가 AND로 연결된다.

p $\wedge \$ q 라고 표기하며 'p and q 또는 p 그리고 q'라고 읽는다.

![image-20230320140326640]({{site.url}}\images\2023-03-20-Review0320-DiscreteMathematics\image-20230320140326640.png)



### OR (논리합, disjunction)

임의의 두 명제 p, q가 OR로 연결된다.

p $\vee \$ q 라고 표기하며 'p or q 나 p 또는 q'라고 읽는다.

![image-20230320140459446]({{site.url}}\images\2023-03-20-Review0320-DiscreteMathematics\image-20230320140459446.png)



### XOR (배타적 논리합, Exclusive OR)

임의의 두 명제 p, q가 XOR로 연결된다.

p $\oplus\$ q 라고 표기하며 'Exclusive OR 또는 XOR'라고 읽는다.

![image-20230320140719069]({{site.url}}\images\2023-03-20-Review0320-DiscreteMathematics\image-20230320140719069.png)



### 조건 (함축, Implication)

임의의 두 명제 p, q의 조건 연산자는 p $\rightarrow\$ q 로 표기하며 'p이면 q이다'라고 읽는다.

![image-20230320140938250]({{site.url}}\images\2023-03-20-Review0320-DiscreteMathematics\image-20230320140938250.png)

뿐만 아니라, 똑같은 진리값을 가지는 다양한 표현으로 나타내어진다.

​	a. p이면 q이다. (if p, then q)

​	b. p는 q의 충분조건이다. (p is sufficient for q)

​	c. q는 p의 필요조건이다. (q is necessary for p)

​	d. p는 q를 함축한다. (p implies q)



### 쌍방 조건

임의의 두 명제 p, q의 쌍방 조건 연산자는 p $\rightarrow\$ q로 펴기하며 'p 이면 q이고, q이면 p이다'라고 읽는다.

p, q 모두 참 또는 거짓일 때 참의 진리값을 가지고 그 외에는 거짓의 값을 갖는다.

![image-20230320141421996]({{site.url}}\images\2023-03-20-Review0320-DiscreteMathematics\image-20230320141421996.png)

쌍방 조건도 마찬가지로 같은 의미를 가진 다른 표현으로 나타내어진다.

​	a. p이면 q이고, q이면 p이다. (p if and only if q)

​	b. p는 q의 필요충분조건이다. (p is necessary and sufficient for q)



### 명제의 상호 관계

![image-20230320141944978]({{site.url}}\images\2023-03-20-Review0320-DiscreteMathematics\image-20230320141944978.png)

명제 p $\rightarrow\$ q에 대하여

p $\rightarrow\$ q 를 **역(converse)**

~p $\rightarrow\$ ~q 를 **이(inverse)**

~q $\rightarrow\$ ~p 를 **대우(contrapositive)**라고 한다.

![image-20230320142152382]({{site.url}}\images\2023-03-20-Review0320-DiscreteMathematics\image-20230320142152382.png)

위의 진리표에서 나타난 것과 같이 다음 관계가 성립한다.

1. 명제와 그의 대우는 논리적 동치 관계이다.

2. 역과 이는 서로 대우 관계이다.

3. 그 이외에는 논리적 동치 관계가 존재하지 않는다.

   



## 항진 명제와 모순 명제

항진 명제(tautology): 단순 명제들의 진리값과 관계없이 합성 명제가 항상 참의 값을 갖는 명제

모순 명제(contradiction): 단순 명제들의 진리값과 관계없이 합성 명제가 항상 거짓의 값을 갖는 명제



## 논리적 동치 관계

논리적 동치(logical equivalence): 임의의 두 명제 p, q가 쌍방조건 p $\leftrightarrow\$ q가 항진 명제이다.

p $\equiv\$q, p $\Leftrightarrow\$ q 라고 표기한다.

두 명제의 논리값이 서로 같으므로 하나의 명제가 다른 명제를 대신 할 수 있다.

![image-20230320142932712]({{site.url}}\images\2023-03-20-Review0320-DiscreteMathematics\image-20230320142932712.png)



## 추론 (Argument)

주어진 명제가 참인 것을 바탕으로 새로운 명제가 참이 되는 것을 유도해내는 방법



유효 추론(valid argument): 주어진 전제가 참이고 결론도 참인 추론

허위 추론(fallacious argument): 주어진 전제가 참이고 결론이 거짓인 추론

이 때 전제를 $p_1\$, $p_2\$, ... , $p_n\$이라 하고 결론을 q라 할 때 수학적 식으로 표시하면 $p_1\$, $p_2\$, ... , $p_n\$ $\vdash\$ q라고 표시한다.

![image-20230320143411727]({{site.url}}\images\2023-03-20-Review0320-DiscreteMathematics\image-20230320143411727.png)



## 술어 논리

명제 중에는 값이 정해지지 않는 변수나 객체가 있어서 참과 거짓을 판별하기 힘든 경우가 있다.



$p(x)\$: 변수 $x\$에 대한 명제 술어(propositional predicate)라 한다.

명제 논리와 구분하여 명제 술어에 대한 논리를 술어 논리(predicate logic)라고 한다.



### 술어 한정자 (predicate quantifier)

전체 한정자: '모든 것에 대하여', $\forall\$

존재 한정자: '존재한다'. $\exists\$

전체 한정자에서 '모든 x에 대하여 $p(x)\$가 성립한다'고 하면, 그의 부정은 '$p(x)\$가 성립하지 않는 x가 존재한다'가 된다.

~($\forall\$$x\$ $p(x)\$) $\Leftrightarrow\$ $\exists\$$x\$(~$p(x)\$)



존재 한정자에서 '$p(x)\$가 성립하는 x가 존재한다.'라고 하면, 그의 부정은 '모든 x는 $p(x)\$가 성립하지 않는다.'가 된다.

~($\exists\$$x\$ $p(x)\$) $\Leftrightarrow\$ $\forall\$$x\$ (~$p(x)\$)
