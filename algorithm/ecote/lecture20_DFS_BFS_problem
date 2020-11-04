# DFS & BFS 기초 문제 풀이 

## <문제> 음료수 얼려 먹기 

### N*M 크기의 얼음 틀이 있다. 구멍이 뚫려있는 부분은 0, 칸막이가 존재하는 부분은 1이다. 구멍이 뚫린 부분끼리 상하좌우로 붙어있는 경우 서로 연결되어 있는 것으로 간주한다. 이때, 얼음 틀의 모양이 주어졌을 때 생성되는 총 아이스크림의 갯수를 구하는 프로그램을 작성하라. 



![image-20201104190631388](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201104190631388.png)

![image-20201104190816537](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201104190816537.png)



##  문제해결 아이디어 

###   DFS 

1. 특정한 지점의 주변 상하좌우를 살핀 뒤에 주변 지점 중에서 값이 '0'이면서 아직 방문하는 지점이 있다면 방문한다. 
2. 방문 지점에서 다시 상하좌우를 살피며 방문을 진행하는 과정을 반복하면, 연결된 모든 지점을 방문할 수 있다. 
3. 모든 노드에 대하여 1~2번의 과정을 반복하여, 방문하지 않은 지점의 수를 카운트 한다. 

```python
# 음료수 얼려먹기

def dfs(x,y):

    if x <=-1 or x>= n  or y <= -1 or y >=m:
        return False

    if graph[x][y]==0:


n, m = map(int, input().split())

graph = []
for i in range(n):
    graph.append(list(map(int, input())))

result = 0
for i in range(n):
    for j in range(m):
        # 현재 위치에서 DFS 수행
        if dfs(i,j) ==True:
            result +=1

print(result)
```



## <문제> 미로 탈출 

- 동빈이는 N * M 크기의 직사각형 미로에 갇혔다. 미로에는 여러 괴물이 있어, 이를 피해 탈출해야 한다. 

- 동빈이 위치는 (1,1)이며, 미로의 출구는 (N,M)이고 한 번에 한 칸씩 이동 가능. 이때 괴물이 있는 칸은 0으로, 괴물이 없는 부분은 1이다. 미로는 반드시 탈출 가능한 형태이다. 

- 이때 동빈이가 탈출하기 위해 움직여야 하는 최소 칸의 갯수는? 칸을 셀 때는 시작칸과 마지막 칸을 모두 포함해서 계산 

  ![image-20201104193713008](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201104193713008.png)

### 문제해결 아이디어

- BFS는 시작 지점부터 가까운 노드부터 차례대로 그래프의 모든 노드를 탐색 
- 상하좌우로 연결된 모든 노드로의 거리가 1로 동일 
  - 따라서 (1,1) 지점부터 BFS를 수행하여 모든 노드의 최단거리 값을 기록하면 된다. 

![image-20201104193921340](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201104193921340.png)

![image-20201104193951666](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201104193951666.png)

![image-20201104194001305](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201104194001305.png)

![image-20201104194025940](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201104194025940.png)

### 미로 탈출 : 답안 예시 

```python
from collections import deque

def bfs(x,y):
    queue = deque()
    queue.append((x,y))

    while queue:
        x, y = queue.popleft()
        # 현재 위치에서 4방향으로 위치 확인

        for i in range(4):

            nx = x +dx[i]
            ny = y +dy[i]

            if nx <0 or nx>= n or ny < 0 or ny>=m:
                continue

            #벽인 경우 무시 (괴물)
            if graph[nx][ny] ==0:
                continue

            # 해당 노드를 처음 방문할때만 최단거리 기록
            if graph[nx][ny] == 1:
                graph[nx][ny] == graph[x][y] +1
                queue.append((nx, ny))
        return graph[n-1][m-1]


n, m = map(int, input().split())
graph = []
for i in range(n):
    graph.append(list(map(int, input())))

# 이동할 4가지 방향 정의
dx = [-1,-1,0,0]
dy = [0,0,-1,1]

# BFS를 수행한 결과 출력
print(bfs(0,0))

```





