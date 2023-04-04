---
layout: single
title:  "Chapter 2. Boolean Algebra & Logic Gates"
categories: DigitalEngineering
tag: [디지털공학, 나작복]
toc: true
author_profile: false
sidebar:
    nav: "docs"
search: true #true, false
use_math: true
---



## Boolean Algebra

### Basic Definitions

1. Closure(닫힘): 

   A set S is closed with respect to a binary operator 
   if, for every pair of elements of S, the binary operator specifies a rule for obtaining a unique elements of S



2. Associative law(결합 법칙):

   (x * y) * z = x * (y * z) for all x, y, z $\in\$ S

   

3. Commutative law(교환 법칙):

   x * y = y * x for all x, y $\in\$ S

   

4. Identity elements(단위 원소):

   e * x = x * e = x, for all x $\in\$ S

   

5. Inverse(역원):

   A set S having the identity elements for all x, y $\in\$ S, x * y = e

   

6. Distributive law(분배 법칙):

   x * (y $\cdot\$ z) = (x * y) $\cdot\$ (x * z)



### Basic theorems & Properties

![image-20230404124835696]({{site.url}}\images\2023-04-05-Review0405-DigitalEngineering\image-20230404124835696.png)

#### Duality

​	Interchange **OR** and **AND** operators and replace 1's by 0's and 0's by 1's



#### Operator precedence

​	Parentheses > NOT > AND > OR



### Boolean functions - Algebraic manipulation

**Simplify the following Boolean functions to a minimum number or literals**

* x(x'+y) = xx' + xy = 0 + xy = xy. 
* x +x'y = (x+x')(x+y) = 1(x+y) = x + y.  
* (x+y)(x+y') = x + xy + xy' + yy' = x(1+y+y') = x.  
* xy + x'z + yz = xy + x'z + yz(x+x') = xy + x'z + xyz + x'yz = xy(1+z) + x'z(1+y) = xy + x'z 
* (x+y)(x'+z)(y+z) = (x+y)(x'+z) : by duality from function 4



**Complement of a function**

(A + B + C)' = (A+x)' : let B+C=x

= A'x' : by theorem (DeMorgan) 

= A'(B+C)' : substitute B+C=x 

= A'(B'C') : by theorem (DeMorgan) 

= **A'B'C'** : by theorem (associative)



How to find the complement of the functions F ?

* Take their duality and complement each literal

-example-

F = x'yz' + z'y'z

The dual of F = (x' + y + z')(x' + y' + z)

Complement each literal F' = (x + y' + z)(x + y + z')



F = x(y'z' + yz)

The dual of F = x + (y' + z')(y + z)

Complement each literal F' = x' + (y + z)(y' + z')



### Canonical & Standard Forms

![image-20230404125706575]({{site.url}}\images\2023-04-05-Review0405-DigitalEngineering\image-20230404125706575.png)

Minterms and Maxterms are the complements



#### Sum of Minterms

F = A + B'C

![image-20230404132548934]({{site.url}}\images\2023-04-05-Review0405-DigitalEngineering\image-20230404132548934.png)

A = A(B + B') = AB(C + C') + AB'(C + C') = ABC + ABC' + AB'C + AB'C'

B'C = B'C(A + A') = AB'C + A'B'C

F = A + B'C = ABC + ABC' + AB'C + AB'C' + AB'C + A'B'C

   = $m_1\$ + $m_4\$ + $m_5\$ + $m_6\$ + $m_7\$

F(A, B, C) = $\sum\$ (1, 4, 5, 6, 7)



#### Product of Maxterms

F = xy + x'z

  = (xy + x')(xy + z) = (x + x')(y + x')(x + z)(y + z) = (x' + y)(x + z)(y + z)

![image-20230404133459089]({{site.url}}\images\2023-04-05-Review0405-DigitalEngineering\image-20230404133459089.png)

x' + y = x' + y + zz' =(x' + y + z)(x' + y + z')

x + z = x + z + yy' = (x + y + z)(x + y' + z)

y + z = y + z + xx' = (x + y + z)(x' + y + z)

F = (x' + y + z)(x' + y + z') (x + y + z)(x + y' + z)(x + y + z)(x' + y + z)

  =$M_0\$$M_2\$$M_4\$$M_5\$

F(x, y, z) = $\prod\$(0, 2, 4, 5)



#### Conversion between Canonical Forms

F(A, B, C) = $\sum\$ (1, 4, 5, 6, 7)

F'(A, B, C) = $\sum\$ (0, 2, 3) = $m_0\$ + $m_2\$ + $m_3\$

F = ($m_0\$ + $m_2\$ + $m_3\$)' = $m_0\$'$m_2\$'$m_3\$' = $M_0\$$M_2\$$M_3\$ = $\prod\$(0, 2, 3)

F(A, B, C) = $\sum\$ (1, 4, 5, 6, 7) = $\prod\$(0, 2, 3)



F(x, y, z) = $\prod\$(0, 2, 4, 5) = $\sum\$ (1, 3, 6, 7)



#### Standard Forms

* Sum of Products : F1 = y' +xy + x'yz' 
* Product of Sums : F2 = x(y'+z)(x'+y+z')

![image-20230404134625974]({{site.url}}\images\2023-04-05-Review0405-DigitalEngineering\image-20230404134625974.png)



-Example-

F3 = AB + C(D+E) = AB +CD + CE

![image-20230404134726694]({{site.url}}\images\2023-04-05-Review0405-DigitalEngineering\image-20230404134726694.png)



## Digital Logic Gates

![image-20230404134817310]({{site.url}}\images\2023-04-05-Review0405-DigitalEngineering\image-20230404134817310.png)

↓ is the symbol for **NOR**

↑ is the symbol for **NAND**



### Extension to Multiple Inputs

The **NAND** and **NOR** operators are not associative.

(xy)↓z ≠ x↓(y↓z) 	: not associative

(x↓y)↓z = [(x+y)'+z]' = (x+y)z'= xz' + yz' $\nleftrightarrow\$ x↓(y↓z)= [x+(y+z)']' = x'(y+z)= x'y + x'z	: not associative



x↓y↓z = (x+y+z)'

x↑y↑z = (xyz)'