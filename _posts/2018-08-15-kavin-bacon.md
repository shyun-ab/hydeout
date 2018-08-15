---
layout: post
title: "케빈 베이컨의 6단계 법칙 (1389)"
categories:
  - Algorithm
commit: true
excerpt_separator:  <!--more-->
---

케빈 베이컨의 6단계 법칙에 의하면 지구에 있는 모든 사람들은 최대 6단계 이내에서 서로 아는 사람으로 연결될 수 있다. 케빈 베이컨 게임은 임의의 두 사람이 최소 몇 단계 만에 이어질 수 있는지 계산하는 게임이다. 유저의 수와 친구 관계가 입력으로 주어졌을 때, 케빈 베이컨의 수가 가장 작은 사람을 구하는 프로그램을 작성하시오. <br>

---
입력받은 친구 관계를 무방향 그래프라고 생각하면 된다. bfs로 각 노드로 가는 최단 거리를 구하고 모두 더한 후 최소값을 구했다!<br>
<br>

```java
for(int i = 1; i <= N; i++) {
    int num = 0;
    Queue<Integer> q = new LinkedList<Integer>();
    boolean isVisited[] = new boolean[N+1];
    int[] f = new int[N+1];

    q.add(i);
    isVisited[i] = true;
    while(!q.isEmpty()) {
        int node = q.remove();
        for(int j = 1; j <= N; j++) {
            if(!isVisited[j] && friend[node][j] == 1) {
                isVisited[j] = true;
                f[j] = f[node] + 1;
                q.add(j);
            }
        }
    }

    for(int k = 1; k <= N; k++) {
        num += f[k];
    }

    list.add(num);
    Answer = Math.min(num, Answer);
}
```
<br>