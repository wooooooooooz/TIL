lecture18_DFS.md



# DFS (Depth-First Search)

## 깊이우선 탐색이라고 부르며, 그래프에서 깊은 부분을 우선적으로 탐색하는 알고리즘 



## 스택 자료구조 (혹은 재귀함수) 를 이용한다 

### 1. 탐색 시작 노드를 스택에 삽입하고 방문처리 

### 2. 스택의 최상단 노드에 방문하지 않은 인접노드가 하나라도 있으면 그 노드를 스택에 넣고 방문처리 

### 3. 방문하지 않은 노드가 하나도 없으면 스택에서 최상단 노드를 꺼낸다 

### 더이상 2번 과정을 수행할 수 없을 때까지 반복 



## DFS 소스코드 예제 

```python
def dfs(graph, v, visted):
    # 현재 노드 방문처리 
    visited[v]= True 
    print(v, end = ' ')
    
    #현재 노드와 연결된 다른 노드를 재귀적으로 방문 
    
    for i in graph[v]:
        if not visited[i]:
            dfs(graph, i, visited)
            

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

# 각 노드가 방문된 정보를 표현 (1차원 리스트)
visited = [False]*9

# 정의된 DFS 함수 호출 
# v : 현재노드 
dfs(graph, 1, visited)

```

