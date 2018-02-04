---
layout: post
title: "Binary Tree"
categories:
  - Algorithm
commit: true
excerpt_separator:  <!--more-->
---

<br>
---
이진 트리(Binary Tree)<br>
- 모든 노드가 최대 2개의 자식을 가질 수 있는 트리<br>

포화 이진 트리(Full Binary Tree)<br>
- 모든 노드가 자식을 둘씩 가지고 있는 이진 트리<br>

완전 이진 트리(Complete Binary Tree)<br>
- 노드들이 트리의 왼쪽부터 채워진 이진 트리<br>

높이 균형 트리(Height Balanced Tree)<br>
- 루트 노드를 기준으로 왼쪽 하위 트리와 오른쪽 하위 트리의 높이가 1 넘게 차이나지 않는 이진 트리<br>

완전 높이 균형 트리(Completely Height Balanced Tree)<br>
- 루트 노드를 기준으로 왼쪽 하위 트리와 오른쪽 하위 트리의 높이가 같은 이진 트리<br>

이진 트리의 순회<br>
- 전위 순회(Preorder Traversal): (1)루트 노드부터 시작해서 아래로 내려오면서 (2)왼쪽 하위 트리를 방문하고, (2)의 방문이 끝나면 (3)오른쪽 하위 트리를 방문<br>
- 중위 순회(Inorder Traversal): (1)왼쪽 하위 트리부터 시작해서 (2)루트를 거쳐 (3)오른쪽 하위 트리를 방문. <br>
- 후위 순회(Postorder Traversal): (1)왼쪽 하위 트리, (2)오른쪽 하위 트리, (3)루트 노드 순으로 방문. 수식 트리를 후위 순회로 출력하면 후위 표기식이 나온다.<br>

---

```c
//중위 순회 출력 함수
void InorderPrintTree(Node* Node){
  if(Node == NULL)
    return;
  
  InorderPrintTree(Node->Left); //왼쪽 하위 트리 출력
  printf(" %c", Node->Data); //루트 노드 출력
  InorderPrintTree(Node->Right); //오른쪽 하위 트리 출력
}
```
