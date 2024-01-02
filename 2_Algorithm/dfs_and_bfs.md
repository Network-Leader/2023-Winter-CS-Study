# DFS/BFS

## 1. 그래프 탐색 알고리즘

### 개념

- 한 정점에서 시작하여 차례대로 그래프에 있는 모든 정점들을 한 번씩 방문하는 알고리즘

### 필요한 경우

- 한 정점과 다른 정점의 경로를 구할 때
- 그래프가 연결되어 있는지 확인할 때
- 신장 트리(spanning tree)를 찾을 때

## 2. DFS

### 정의

- 깊이 우선 탐색
- 스택과 재귀를 이용함
- 처음 시작하는 노드를 스택에 push
- 인접 노드를 스택에 push
- 스택의 최상단 노드가 방문하지 않은 인접 노드를 방문
- 현재 노드와 연결된 노드들 중 이동할 노드가 하나도 없다면, 다시 전 단계의 노드로 되돌아감 (pop)
- 이를 끝날 때까지 계속 반복

![dfs](https://github.com/Network-Leader/2023-Winter-CS-Study/assets/49124725/289a22de-141b-416f-9536-26bcb0a7272b)

### 장점

- 현 경로상의 노드들만 기억하면 되므로 저장공간 수요가 비교적 적음
- 목표 노드가 깊은 단계에 있을 경우 해를 빨리 구할 수 있음

### 단점

- 해가 없는 경로가 깊을 경우 탐색 시간이 오래 걸림
- 얻어진 해가 최단 경로가 된다는 보장이 없음
- 깊이가 무한히 깊어지면 스택오버플로우의 가능성 존재(깊이 제한을 두는 방법으로 해결 가능)
  <br/>

### 구현

#### 인접 행렬 (모든 정점을 순회하며 간선의 존재 여부 확인)

```
vector<vector<int>> adjacent; //인접 행렬로 구현된 그래프
vector<bool> visited; // 그래프의 정점 크기로 생성

void DFS(int now)
{
  visited[now] = true;
  for (int i = 0; i < adjacent.size(); i++)
  {
    if (adjacent[now][i] == 0)
      continue;
    if (!visited[i])
      DFS(i);
  }
}
```

- 시간복잡도
  DFS 하나당 N번의 loop를 돌게 되므로 O(N)의 시간복잡도
  N개의 정점을 모두 방문 해야하므로 N\*O(N)
  -> O(N^2)

#### 인접 리스트 (현재 정점과 연결된 정점을 순회하며 방문 여부 확인)

```
vector<vector<int>> adjacent; //인접 리스트로 구현된 그래프
vector<bool> visited; // 그래프의 정점의 크기로 생성

void DFS(int now)
{
visited[now] = true;

    for (int i = 0; i < adjacent[now].size(); i++)
    {
    	int next = adjacent[now][i];
    	if (!visited[next])
    		DFS(next);
    }

}
```

- 시간복잡도
  DFS가 총 N번 호출, 하지만 DFS하나당 각 정점에 연결되어 있는 간선의 개수만큼 탐색을 하게 되므로 예측이 불가능
  DFS가 다 끝난 경우, 모든 정점을 한번씩 다 방문 & 모든 간선을 한번씩 모두 검사
  ->O(N+E)
  <br/>

## 3. BFS

### 정의

- 너비 우선 탐색
- 큐 이용
- 탐색 시작 노드를 큐에 삽입하고 방문 처리 함
- 큐에서 노드를 꺼낸 뒤 해당 노드의 인접 노드 중에서 방문하지 않은 노드를 큐에 삽입
- 이를 끝날 때까지 계속 반복

![bfs](https://github.com/Network-Leader/2023-Winter-CS-Study/assets/49124725/daa019d4-64e1-4587-9167-1efea1b41f67)

### 장점

- 답이 되는 경로가 여러 개인 경우에도 최단 경로를 얻을 수 있음
- 경로가 무한히 깊어져도 최단 경로를 반드시 찾을 수 있음
- 노드 수가 적고 깊이가 얕은 해가 존재할 때 유리

### 단점

- 큐를 이용하여 다음에 탐색할 정점들을 저장하므로 더 큰 저장공간이 필요
  <br/>

### 구현

#### 인접 행렬

```
vector<vector<int>> adjacent; //인접 행렬로 구현된 그래프
vector<bool> visited; //그래프의 정점 크기로 생성

void BFS(int now)
{
  queue<int> q;
  q.push(now);
  visited[now] = true;
  while(!q.empty())
  {
    now = q.front();
    q.pop();
    for (int i = 0; i < adjacent.size(); i++)
    {
      if (adjacent[now][i] == 0) //간선의 존재 여부 확인
        continue;
      if (!visited[i])
      {
        q.push(i);
        visited[i] = true;
      }
    }
  }
}
```

- 시간복잡도
  정점 한개당 N번의 loop를 돌기 때문에 O(n)의 시간 소요
  loop는 큐에 아무것도 없을 때까지(=모든 정점을 방문할 때까지) 실행되므로 n번 반복 실행
  -> O(n^2)

#### 인접 리스트

```
vector<vector<int>> adjacent; //인접 리스트로 구현된 그래프
vector<bool> visited; //그래프의 정점 크기로 생성

void BFS(int now)
{
queue<int> q;

    q.push(now);
    visited[now] == true;

    while(!q.empty())
    {
    	now = q.front();
    	q.pop();

    	for (int i = 0; i < adjacent[now].size(); i++)
    	{
    		int next = adjacent[now][i];
    		if (!visited[next]) //방문 여부 확인
    		{
    			q.push(next);
    			visited[next] = true;
    		}
    	}
    }
}
```

- 시간복잡도
  BFS가 다 끝난 경우, 모든 정점을 한번씩 다 방문 & 모든 간선을 한번씩 모두 검사
  ->O(n+e)
  <br/>

## 참고자료

https://currygamedev.tistory.com/10  
https://catch-me-java.tistory.com/43
