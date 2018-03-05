---
layout: post
title: "Expression Tree"
categories:
  - Algorithm
commit: true
excerpt_separator:  <!--more-->
---

<br>
---
수식 트리(Expression Tree)<br>
- 피연산자: 잎 노드<br>
- 연산자: 루트 노드 또는 가지 노드<br>

---

```c
switch(Tree->Data){

//연산자인 경우
case '+': case '-': case '*': case '/':
   Left = Evaluate(Tree->Left);
   Right = Evaluate(Tree->Right);
   
   if(Tree->Data == '+') Result = Left + Right;
   // else if ... '-', '*', '/' (방식 동일)
   break;
   
//피연산자인 경우
default :
   memset(Temp, 0, sizeof(temp));
   Temp[0] = Tree->Data;
   Result = atof(Temp);
   break;
   
}
```
