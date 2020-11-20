# 최단 경로 알고리즘 기초 문제 풀이 

## 전보 : 문제설명 

- 아떤 나라에는 N개의 도시가 있다. 그리고 각 도시는 보내려는 메시지가 있는 경우, 다른 도시로 전보를 보내서 메시지를 전송 가능하다. 
- 하지만 X라는 도시에서 Y라는 도시로 전보를 보내고자 한다면, 도시X 에서 Y로 향하는 통로가 있어야 한다. 또한 통로를 거쳐 메시지를 보낼 때는 일정시간이 소요된다. 
- C라는 도시에 위급상황이 발생하여, 최대한 많은 도시로 메시지를 보내고자 한다. 메시지는 __C에서 출발하여 각 도시 사이에 설치된 통로를 거쳐, 최대한 많이 퍼져나갈 것__이다. 
- 각 도시의 번호와 통로가 설치되어 있는 정보가 주어졌을 때, 도시 C에서 보낸 메시지를 받게 되는 도시의 개수는 총 몇개이며 도시들이 모두 메시지를 받는 데까지 걸리는 시간은 얼마인지 계산하는 프로그램을 작성 

![image-20201120215909543](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201120215909543.png)

## 문제 해결 아이디어 

- __핵심 아이디어__ : 한 도시에서 다른 도시까지의 최단 거리 문제로 치환 
- N과 M의 범위가 충분히 크기 때문에 우선순위 큐를 활용한 다익스트라 알고리즘을 구현 

![image-20201120220058786](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201120220058786.png)

### 전보 : 답안 예시

```python
import heapq
import sys

input = sys.stdin.readline

INF = int(1e9)


def dijkstra(start):
    q = []

    heapq.heappush(q, (0,start))
    distance[start] = 0

    while q:
        dist, now = heapq.heappop(q)
        if distance[now] < dist:
            continue
        for i in graph[now]:
            cost = dist +i[1]
            if cost < distance[i[0]]:
                distance[i[0]] = cost
                heapq.heappush(q, (cost, i[0]))

n, m, start = map(int, input().split())

graph = [[] for i in range(n+1)]
distance = [INF] * (n+1)

for _ in range(m):
    x,y,z = map(int, input().split())
    graph[x].append((y,z))

dijkstra(start)

count = 0
max_distance = 0

for d in distance:
    if d != 1e9
        count += 1
        max_distance = max(max_distance,d)

print(count-1, max_distance)
```



## 미래 도시 : 문제 설명 

- 미래 도시에는 1번부터 N번 까지의 회사가 있는데 특정 회사끼리는 서로 도로를 통해 연결되어 있다. 방문 판매원 A는 현재 1번 회사에 위치해 있으며, X번 회사에 방문해 물건을 판매하고자 한다. 
- 미래 도시에서 특정 회사에 도착하기 위한 방법은 회사끼리 연결되어 있는 도로를 이용하는 방법이 유일하다. 또한 연결된 2개의 회사는 __양방향__으로 이동할 수 있다. 공중 미래도시에서 특정 회사가 도로로 연결되어 있다면, 정확히 1만큼의 시간으로 이동할 수 있다. 
- 또한 오늘 방문 판매원 A는 기대하던 소개팅에도 참석하고자 한다. 소개팅의 상대는 K번 회사에 존재한다. 방문 판매원 A는 X번 회사에 가서 물건을 판매하기 전에 먼저 소개팅 상대의 회사에 찾아가서 함께 커피를 마실 예정이다. 따라서 방문 판매원 A는 __1번 회사에서 출발하여 K번 회사를 방문한 뒤에 X번 회사로 가는 것이 목표__다. 이떄 방문 판매원 A는 가능한 한 빠르게 이동하고자 한다. 
- 방문 판매원이 회사 사이를 이동하게 되는 __최소 시간__을 계산하는 프로그램을 작성하시오 

![image-20201120221450831](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201120221450831.png)

### 미래 도시 : 문제 해결 아이디어 

- __핵심 아이디어__ : 최단 거리 알고리즘 
- N의 크기가 최대 100이므로 플로이드 워셜을 이용해도 효율적 
- 플로이드 워셜을 수행한 뒤 __(1번 노드에서 X까지의 최단 거리 + X에서 K 까지의 최단거리)__를 계산하여 출력하면 정답 

```python
INF = int(1e9)
n,m = map(int, input().split())


graph = [[INF]*(n+1) for _ in range(n+1)]

for a in range(1, n+1):
    for b in range(1, n+1):
        if a==b:
            graph[a][b] = 0

for _ in range(m):
    a,b = map(int, input().split())
    graph[a][b] = 1
    graph[b][a] = 1

x,k = map(int, input().split())

for k in range(1, n+1):
    for a in range(1, n + 1):
        for b in range(1, n+1):
            graph[a][b] = min(graph[a][b], graph[a][k], graph[k][b])

distance = graph[1][k] +graph[k][x]

if distance >= INF:
    print("-1")

else:
    print(distance)
```

