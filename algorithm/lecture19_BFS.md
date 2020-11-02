# BFS (Breadth-First Search)

## BFS는 너비 우선 탐색 이라고 부르며, 그래프에서 가까운 노드부터 우선적으로 탐색하는 알고리즘 

1. 탐색 시작 노드를 큐에 삽입하고 방문 처리 
2. 큐에서 노드를 꺼낸 뒤에 해당 노드의 인접 노드 중에서 방문하지 않은 노드를 모두 큐에 삽입하고 방문 처리 
3. 더 이상 2번의 과정을 수행할 수 없을 때까지 반복



## BFS 소스코드 예제 

```python
from collections import deque 

# BFS 메서드 정의 
def bfs(graph, start, visited)
	queue = deque([start])
    
    visited[start] = True
    
    while queue:
        v = queue.popleft() 
        print(v, end ='')
        
        for i in graph[v]:
            if not visited[i]:
                queue.append(i)
                visited[i] = True
                
graph = [
    [],
    [2,3,8],
    [1,7],
    [1,4,5],
    [3,5],
    [3,4],
    [7],
    [2,6,8],
    [1,7]
]

# 각 노드가 방문된 정보를 표현 
visited = [False]*9 

# 정의된 BFS 함수 호출 
bfs(graph, 1 , visited)
```

