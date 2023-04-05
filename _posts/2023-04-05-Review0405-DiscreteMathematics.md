---
layout: single
title:  "Chapter 4. 증명법"
categories: DiscreteMathematics
tag: [이산수학, 나작복]
toc: true
author_profile: false
sidebar:
    nav: "docs"
search: true #true, false
use_math: true
---



## 증명 (Proof)

논리적 법칙을 이용하여 주어진 **가정**으로부터 **결론**을 유도해내는 추론의 한 방법으로서, 어떠한 명제나 논증이 적절하고 타당한 지를 입증하는 작업이다.



**증명의 단계적 접근 방법**

1. 아이디어 스케치 단계
   * 문제 해결의 핵심적인 실마리를 찾아내어 기술함.

2. 구체적인 방법론 제시 단계
   * 아이디어를 묶어서 구체적인 블록 다이어그램(Block Diagram) 등으로 표현함.
   * 프로그래밍의 경우 유사 코드 (Pseudo Code) 단계까지 구체화하는 단계.

3. 엄밀한 입증이나 증명의 단계
   * 자기가 내린 결론을 객관적인 증명 방법을 통해 누구나 공감할 수 있게 증명함.



## 증명 방법

수학이나 공학에서의 증명 문제는 p $\rightarrow\$ q 와 같은 논리 함축을 증명함.

논리 함축 p $\rightarrow\$ q가 참이 되기 위해서는 **p, q가 모두 참**이거나 **q에 관계없이 p가 거짓**임을 보이면 된다.



* 연역법

  주어진 사실들과 공리들에 입각하여 추론을 통하여 새로운 사실을 도출하는 것

* 귀납법

  관찰과 실험에 기반한 가설을 귀납 추론을 통하여 일반적인 규칙을 입증하는 것



### 수학적 귀납법 (Mathematical Induction)

명제 $p_1\$, $p_2\$, $p_3\$, ... , $p_n\$이 사실이라고 할 때, $p_{n+1}\$의 경우에도 성립함을 보이면 된다.

먼저, n이 1인 경우에 성립하는 것을 보이고, 모든 양의 정수 n에 대해 성립한다고 가정하면 n+1의 경우에도 성립함을 보여주면 된다.

**기초 단계 (basis)**

​	출발점이 되는 n의 값

**귀납 가정 (inductive assumption)**

​	$p_1\$, $p_2\$, $p_3\$, ... , $p_n\$이 성립한다고 가정

**귀납 단계 (inductive step)**

​	$p_{n+1}\$의 경우에도 성립

![image-20230405204919240]({{site.url}}\images\2023-04-05-Review0405-DiscreteMathematics\image-20230405204919240.png)



### 모순 증명법 (Proof by Contradiction)

주어진 문제의 명제를 부정해 놓고 논리를 전개함.

그 결과 모순됨을 보임으로써 본래의 명제가 사실임을 증명하는 방법이다.

p $\rightarrow\$ q가 참인 것과 p $\land\$ (~q)가 거짓임은 동치이므로  p $\land\$ (~q)가 참이라고 가정하고, 그 결과 모순이 유도되면 원래의 명제가 참임을 증명한 셈이다.

![image-20230405205155015]({{site.url}}\images\2023-04-05-Review0405-DiscreteMathematics\image-20230405205155015.png)



### 직접 증명법 (Direct Proof)

명제 p $\rightarrow\$ q의 직접 증명은 논리적으로 p의 진리 값이 참일 때 q도 참임을 보이는 증명 방법이다.

![image-20230405205315009]({{site.url}}\images\2023-04-05-Review0405-DiscreteMathematics\image-20230405205315009.png)



### 대우 증명법 (Contrapositive Proof)

p $\rightarrow\$ q와 ~q $\rightarrow\$ ~p가 대우 관계로서 논리적 동치가 됨을 이용하여, ~q $\rightarrow\$ ~p가 참인 것을 증명하는 방법이다.

p $\rightarrow\$ q가 참이 되는 것을 논리적 동치 관계를 이용하여 간접적으로 보여 주는 증명 방법이다.

![image-20230405205632188]({{site.url}}\images\2023-04-05-Review0405-DiscreteMathematics\image-20230405205632188.png)



### 존재 증명법 (Existence Proof)

$p(x)\$를 $x\$라는 변수를 가지는 명제라고 한다면 $p(x)\$가 참인 $x\$가 적어도 하나가 존재한다는 것을 보이는 증명 방법이다.

$\exists\$$x\$ such that $p(x)\$

![image-20230405205835458]({{site.url}}\images\2023-04-05-Review0405-DiscreteMathematics\image-20230405205835458.png)



### 반례 증명법 (Proof by Counter-Example)

어떤 명제가 참 또는 거짓임을 입증하기 어려운 경우에 효과적인 증명 방법이다.

주어진 명제에서 모순이 되는 간단한 하나의 예를 보임으로써 비교적 쉽게 증명할 수 있는 방법이다.

$\forall\$x $p(x)\$이 거짓임을 보이기 위해 ~[$\forall\$x $p(x)\$]와 동치인 $\exists\$x ~$p(x)\$에서 $p(x)\$가 만족하지 않는 $x\$가 적어도 하나 존재함을 보인다.

이 경우 $x\$를 **반례**라고 한다.

![image-20230405210139009]({{site.url}}\images\2023-04-05-Review0405-DiscreteMathematics\image-20230405210139009.png)



### 필요충분조건 증명법 (If and Only If Proof)

주어진 명제의 동치를 통하여 증명한다.

'p if and only if q'를 증명하기 위해 '만약 p이면 q이다'와 '만약 q이면 p이다'의 두 가지를 증명한다.

p $\leftrightarrow\$ q $\equiv\$ (p $\rightarrow\$ q) $\land\$ (q $\rightarrow\$ p)

![image-20230405210641624]({{site.url}}\images\2023-04-05-Review0405-DiscreteMathematics\image-20230405210641624.png)
