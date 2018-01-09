---
layout: post
title: "Linked List (Circular-Doubly)"
categories:
  - Algorithm
commit: true
excerpt_separator:  <!--more-->
---

01/10 Doubly Linked List & Circular DLL 끝!<br>
<br>
어쩌다보니 이 글이 2018년 새 글이 되었다! 가족여행을 다녀오는 바람에 그동안 공부를 버려뒀다....ㅎ 이번 달에 또 여행에 2월에는 정해진 일정도 있고 공부도 해야하는데... 바쁘다 바빠<br>

---
더블 링크드 리스트의 특징<br>
- 이전 노드를 가리키는 포인터를 추가해 양방향 탐색이 가능<br>

환형 더블 링크드 리스트의 특징<br>
- Head는 PrevNode로 Tail을, Tail은 NextNode로 Head를 가리킴<br>
- Tail에 접근하는 비용이 다른 링크드 리스트들에 비해서 엄청나게 작아지므로 맨 뒤에 노드를 추가하는 함수, 뒤에서부터 노트를 탐색하는 함수 등의 성능이 획기적으로 개선됨<br>
- 빈 리스트에 새 노드를 추가하면 Head의 PrevNode, NextNode 모두 Head 자신이 됨<br>

---

```c
int GetNodeCount(Node* Head) {
	unsigned int	Count	= 0;
	Node*			Current = Head;

	while (Current != NULL) {
		Current = Current->NextNode;
		Count++;

		//환형 링크드 리스트에서는 무한반복 하게 되므로 Head에서 break를 해주어야 함!
		if (Current == Head)
			break;
	}

	return Count;
}
```
환형 링크드 리스트를 이용할 때는 무한루프에 빠지는 것을 조심해야 할 것 같다.