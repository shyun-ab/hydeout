---
layout: post
title: "Parenthesis Pairs"
categories:
  - Algorithm
commit: true
excerpt_separator:  <!--more-->
---

Given an integer N, find the number of possible balanced parentheses with N opening and closing brackets. <br>

---
이게 제일 기본적인 문제인데 맨날 헷갈린다 참나..... <br>
이건 엄청 금방 풀어야하는데 왜 오래 걸리는지..ㅠㅠ 좀 더 익숙해질 필요가 있을 것 같다. <br>
재귀함수를 사용하는 아주 전형적인 문제이다. "("와 ")"를 더할 때마다 각각의 개수를 잘 알고 있어야 한다. 닫는 괄호의 개수는 여는 괄호의 개수보다 커질 수 없고, 다 더한 string의 글자 수가 입력받은 N의 2배와 같으면 list에 추가하고 return해서 그 다음 string으로 넘어간다. <br>
<br>

```java
static void recurse(List<String> list, String str, int open, int close) {
	if(str.length() == N*2) {
		list.add(str);
		return;
	}

    if(open < N) recurse(list, str + "(", open + 1, close);
	if(close < open) recurse(list, str + ")", open, close + 1);
}
```
