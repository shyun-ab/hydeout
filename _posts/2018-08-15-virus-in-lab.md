---
layout: post
title: "연구소 (14502)"
categories:
  - Algorithm
commit: true
excerpt_separator:  <!--more-->
---

벽을 3개 세운 뒤, 바이러스가 퍼질 수 없는 곳을 안전 영역이라고 한다. 연구소의 지도가 주어졌을 때 얻을 수 있는 안전 영역 크기의 최대값을 구하는 프로그램을 작성하시오. <br>

---
이 문제는 예전에 알고리즘을 막 처음 공부하기 시작했을 때는 못 풀었던 문제인데 dfs와 bfs를 명확히 하고 나니 쉬운 문제였다. <br>
벽을 dfs로 3개까지 세우고, bfs로 바이러스를 퍼뜨리면 된다.<br>
<br>

```java
static void dfs(int count) {
	if(count == 3) {
		bfs();
		return;
	}

	for(int i = 0; i < N; i++) {
		for(int j = 0; j < M; j++) {
			if(map[i][j] == 0) {
				map[i][j] = 1;
				dfs(count + 1);
				map[i][j] = 0;
			}
		}
	}
}
```
<br>
```java
static void bfs() {
	int tmp = 0;
	int[][] tmpmap = new int[N][M];
	Queue<Integer> q = new LinkedList<Integer>();

	for(int i = 0; i < N; i++) {
		for(int j = 0; j < M; j++) {
			tmpmap[i][j] = map[i][j];
			if(tmpmap[i][j] == 2) {
				q.add(i);
				q.add(j);
			}
		}
	}

	while(!q.isEmpty()) {
		int x = q.remove();
		int y = q.remove();

		if(x-1 >= 0 && tmpmap[x-1][y] == 0) {
			tmpmap[x-1][y] = 2;
			q.add(x-1);
			q.add(y);
		}
		if(x+1 < N && tmpmap[x+1][y] == 0) {
			tmpmap[x+1][y] = 2;
			q.add(x+1);
			q.add(y);
		}
		if(y-1 >= 0 && tmpmap[x][y-1] == 0) {
			tmpmap[x][y-1] = 2;
			q.add(x);
			q.add(y-1);
		}
		if(y+1 < M && tmpmap[x][y+1] == 0) {
			tmpmap[x][y+1] = 2;
			q.add(x);
			q.add(y+1);
		}
	}

	for(int k = 0; k < N; k++) {
		for(int l = 0; l < M; l++) {
			if(tmpmap[k][l] == 0) tmp++;
		}
	}

	Answer = Math.max(tmp, Answer);
}
```
<br>