---
layout: single
title:  "Chapter 3. Gate-Level Minimaization"
categories: DigitalEngineering
tag: [디지털공학, 나작복]
toc: true
author_profile: false
sidebar:
    nav: "docs"
search: true #true, false
use_math: true
---



## Map method

### Rule of K-map simplification

* Adjacent squares can be combined as the number of $2^n\$ such as 1, 2, 4, 8, ...
* All minterms need to be covered
* Maximize the number of combined squares in a product term(=group)
* Minimize the number of the product terms(=group)



### Two-variable

![image-20230408191839269]({{site.url}}\images\2023-04-08-Review0408-DigitalEngineering\image-20230408191839269.png)

### Three-variable

![image-20230408191853821]({{site.url}}\images\2023-04-08-Review0408-DigitalEngineering\image-20230408191853821.png)

### Four-variable

![image-20230408191913714]({{site.url}}\images\2023-04-08-Review0408-DigitalEngineering\image-20230408191913714.png)

### Prime implicants

a product term obtained by combining the maximum possible number of adjacent squares.

A prime implicant is essential if it is the only prime implicant that covers the minterm.

![image-20230408192518666]({{site.url}}\images\2023-04-08-Review0408-DigitalEngineering\image-20230408192518666.png)



## Product of Sum simplifications

F(A, B, C, D) = $\sum\$(0, 1, 2, 5, 8, 9, 10)

​	Sum of Products: F = B'D' + B'C' + A'C'D

​	Product of Sums: F = (A'+ B')(C' + D')(B' + D)

![image-20230408193215617]({{site.url}}\images\2023-04-08-Review0408-DigitalEngineering\image-20230408193215617.png)

​	Complement of F: F' = AB + CD + BD'

​	Complement of F': (F')' = (A'+ B')(C' + D')(B' + D) = Product of Sums



## Don't care conditions

F(w, x, y, z) = $\sum\$(1, 3, 7, 11, 15)

Don't care conditions, d(w, x, y, z) = $\sum\$(0, 2, 5)

![image-20230408193901084]({{site.url}}\images\2023-04-08-Review0408-DigitalEngineering\image-20230408193901084.png)

F1(w, x, y, z) = $\sum\$(0, 1, 2, 3, 7, 11, 15)

F2(w, x, y, z) = $\sum\$(1, 3, 5, 7, 11, 15)



## NAND & NOR implementation

#### NAND circuits

![image-20230408194201608]({{site.url}}\images\2023-04-08-Review0408-DigitalEngineering\image-20230408194201608.png)

#### NAND implementation

F = AB + CD

  =((AB)'(CD)')'

![image-20230408194321093]({{site.url}}\images\2023-04-08-Review0408-DigitalEngineering\image-20230408194321093.png)



#### NOR circuits

![image-20230408194435389]({{site.url}}\images\2023-04-08-Review0408-DigitalEngineering\image-20230408194435389.png)



#### NOR implementation

F = (A + B)(C + D)E

  = ((A + B)' + (C + D)' + E)'

![image-20230408195006745]({{site.url}}\images\2023-04-08-Review0408-DigitalEngineering\image-20230408195006745.png)



## Exclusive-OR function

* x $\oplus\$ y = xy' + x'y
* (x $\oplus\$ y)' = (xy' + x'y)' = xy + x'y'
* x $\oplus\$ 0 = x
* x $\oplus\$ 1 = x'
* x $\oplus\$ x = 0
* x $\oplus\$ x' = 1
* x $\oplus\$ y' = x' $\oplus\$ y = (x $\oplus\$ y)'
* A $\oplus\$ B = B $\oplus\$ A :Commutative law
* (A $\oplus\$ B) $\oplus\$ C = A $\oplus\$ (B $\oplus\$ C) = A $\oplus\$ B $\oplus\$ C :Associatie law



#### implementation with NAND Gates

![image-20230408195528149]({{site.url}}\images\2023-04-08-Review0408-DigitalEngineering\image-20230408195528149.png)



### Odd function

A $\oplus\$ B $\oplus\$ C = $\sum\$(1, 2, 4, 7)

![image-20230408195635357]({{site.url}}\images\2023-04-08-Review0408-DigitalEngineering\image-20230408195635357.png)

A $\oplus\$ B $\oplus\$ C $\oplus\$ D = $\sum\$(1, 2, 4, 7, 8, 11, 13, 14)

![image-20230408195816212]({{site.url}}\images\2023-04-08-Review0408-DigitalEngineering\image-20230408195816212.png)



### Even function

A $\oplus\$ B $\oplus\$ C = $\sum\$(0, 3, 5, 6)

![image-20230408195723824]({{site.url}}\images\2023-04-08-Review0408-DigitalEngineering\image-20230408195723824.png)

A $\oplus\$ B $\oplus\$ C $\oplus\$ D= $\sum\$(0, 3, 5, 6, 9, 10, 12, 15)

![image-20230408195910266]({{site.url}}\images\2023-04-08-Review0408-DigitalEngineering\image-20230408195910266.png)



### Parity generation and Checking

* Even parity generator: P = x $\oplus\$ y $\oplus\$ z

![image-20230408200011343]({{site.url}}\images\2023-04-08-Review0408-DigitalEngineering\image-20230408200011343.png)

* Even parity checker: C = x $\oplus\$ y $\oplus\$ z $\oplus\$ P

<img src="{{site.url}}\images\2023-04-08-Review0408-DigitalEngineering\image-20230408200050002.png" alt="image-20230408200050002" style="zoom:125%;" />
