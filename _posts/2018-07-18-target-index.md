---
layout: post
title: "Target Index"
categories:
  - Algorithm
commit: true
excerpt_separator:  <!--more-->
---

정수 배열과 타겟 숫자가 주어지면, 합이 타겟값이 되는 두 원소의 인덱스를 찾으시오. 시간복잡도는 O(n)으로 한다. <br>

---
문제의 요구사항이 너무 불친절해서... 뭘 말하는 지는 알겠는데 조건이 제대로 나와있지 않아서 그냥 대충 풀었다.. 근데 풀이에 나와있는 해쉬맵을 이용하는 방법은 꼭 기억해두고 싶어서 정리한다. <br>
해쉬맵을 사용해서 <배열 원소 값, 인덱스>를 저장하면 된다. 타겟값에서 현재 원소 값을 뺀 뒤 그것을 키값으로 현재까지 저장한 배열에 있었는지를 먼저 찾는다! 있으면 두 인덱스를 리턴하고, 없으면 현재 원소 값과 인덱스를 해쉬맵에 저장한다.<br>
<br>

```java
Map<Integer, Integer> map = new HashMap<>();
for(int i = 0; i < arr.length; i++) {
	int comp = target - arr[i];
	if(map.containsKey(comp)) {
		System.out.println(map.get(comp) + " " + i);
		solution = true;
	}
	map.put(arr[i], i);
}
```
<br>