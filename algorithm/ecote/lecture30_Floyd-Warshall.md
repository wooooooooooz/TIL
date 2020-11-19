# 플로이드 워셜 알고리즘 개요

- __모든 노드에서 다른 모든 노드까지의 최단 경로를 모두 계산__합니다
- 플로이드 워셜 알고리즘은 다익스트라 알고리즘과 마찬가지로 단계별로 __거쳐가는 노드를 기준으로 알고리즘을 수행__합니다.
  - 다만 매 단계마다 방문하지 않은 노즈 중에 최단 거리를 갖는 노드를 찾는 과정이 필요하지 않습니다.
- 플로이드 워셜은 2차원 테이블에 최단 거리 정보를 저장합니다.
- 플로이드 워셜 알고리즘은 다이나믹 프로그래밍 유형에 속합니다. 

## 플로이드 워셜 알고리즘 

- 각 단계마다 __특정한 노드 k를 거쳐가는 경우를 확인__합니다 
  - a에서 b로 가는 최단 거리보다 a에서 k를 거쳐 b로 가는 거리가 더 짧은 지 검사 
- 점화식은 다음과 같다 
  - D<sub>ab</sub> = min(D<sub>ab</sub>, D<sub>ak</sub> + D<sub>kb</sub>)

## 플로이드 워셜 알고리즘 : 동작 과정 살펴보기 

- ​	[초기상태] 그래프를 준비하고 최단 거리 테이블을 초기화 
  - 기본 점화식 : D<sub>ab</sub> = min(D<sub>ab</sub>, D<sub>ak</sub> + D<sub>kb</sub>)

![image-20201120002801486](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201120002801486.png)

- [Step 1 ] 1번 노드를 거쳐가는 경우를 고려하여 테이블을 갱신 
  - 점화식 :  D<sub>ab</sub> = min(D<sub>ab</sub>, D<sub>ak</sub> + D<sub>kb</sub>)

![image-20201120002859791](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201120002859791.png)

- [Step 2] 2번 노드를 거쳐가는 경우를 고려하여 테이블을 갱신합니다. 
  - 점화식 :  D<sub>ab</sub> = min(D<sub>ab</sub>, D<sub>ak</sub> + D<sub>kb</sub>)

![image-20201120002942215](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201120002942215.png)

[Step 3] 3번 노드를 거쳐가는 경우를 고려하여 테이블을 갱신합니다. 

- 점화식 :  D<sub>ab</sub> = min(D<sub>ab</sub>, D<sub>ak</sub> + D<sub>kb</sub>)

![image-20201120003008708](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201120003008708.png)

[Step 4] 4번 노드를 거쳐가는 경우를 고려하여 테이블을 갱신합니다. 

- 점화식 :  D<sub>ab</sub> = min(D<sub>ab</sub>, D<sub>a4</sub> + D<sub>4b</sub>)

![image-20201120003052229](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201120003052229.png)

### 플로이드 워셜 알고리즘 

```python
INF  = int(1e9)

n = int(input())
m = int(input())

graph = [[INF]* (n+1) for _ in range(n+1)]

for a in range(1, n+1):
    for b in range(1, n+1):
        if a ==b:
            graph[a][b] = 0

for _ in range(m):
    a,b,c = map(int, input().split())
    graph[a][b] = c

for k in range(1, n+1):
    for a in range(1, n+1):
        for b in range(1, n+1):
            graph[a][b] = min(graph[a][b],graph[a][k] +graph[k][b])

for a in range(1, n+1):
    for b in range(1, n+1):
        if graph[a][b] == INF:
            print("INFINITY" ,end = " ")
        else:
            print(graph[a][b], end = " ")
        print()
```



### 플로이드 워셜 알고리즘 성능 분석 

- 노드의 개수가 N개일때 알고리즘 상 으로 N번의 단계를 수행합니다.

  - 각 단계마다 O(N^2)의 연산을 통해 현재 노드를 거쳐가는 모든 경로를 고려합니다.

- 따라서 플로이드 워셜 알고리즘의 총 시간 복잡도는 O(N<sup>3</sup>) 이다. 

  

