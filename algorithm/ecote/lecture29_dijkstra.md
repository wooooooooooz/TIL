최단경로 알고리즘 
최단 경로 알고리즘은 가장 짧은 경로를 찾는 알고리즘을 의미 

다양한 문제 상황 

한 지점에서 다른 한 지점까지의 최단 경로 

한 지점에서 다른 모든 지점까지의 최단 경로 

모든 지점에서 다른 모든 지점 까지의 최단 경로 

각 지점은 그래프에서 노드로표현 

지점 간 연결된 도로는 그래프에서 간선으로 표현 

image-20201118220505966

다익스트라 최단 경로 알고리즘 개요 
특정한 노드에서 출발하여 다른 모든 노드로 가는 최단 경로를 계산 

다익스트라 최단 경로 알고리즘은 음의 간선이 없을때 정상적으로 동작

현실 세계의 도로(간선)은 음의 간선으로 표현되지 않음 

다익스트라 최단 경로 알고리즘은 그리디 알고리즘으로 분류 

매 상황에서 가장 비용이 적은 노드를 선택해 임의의 과정을 반복합니다. 

알고리즘의 동작과정은 다음과 같습니다.

출발 노드 설정 

최단 거리 테이블 초기화 

방문하지 않은 노드 중에서 최단 거리가 가장 짧은 노드를 선택 

해당 노를 거쳐 다른 노드로 가는 비용을 계산해 최단 거리 테이블을 갱신 

3,4번 반복 

알고리즘 동작 과정에서 최단 거리 테이블은 각 노드에 대한 현재까지의 최단 거리 정보를 갖고 있음 

처리 과정에서 더 짧은 경로를 찾으면 '이제 부터는 이 경로가 제일 짧은 경로야'라고 갱신 합니다. 

image-20201118221315643

image-20201118221330030

다익스트라 알고리즘 : 동작 과정 살펴보기 
[초기 상태] 그래프를 준비하고 출발 노드를 설정 

image-20201118221422924

image-20201118221433988

image-20201118221456610

image-20201118221518812

image-20201118221531425

image-20201118221543922

image-20201118221600854

다익스트라 알고리즘의 특징 
그리디 알고리즘 : 매 상황에서 방문하지 않는 가장 비용이 적은 노드를 선택해 임의의 과정을 반복합니다. 

단계를 거치며 한 번 처리된 노드의 최단거리는 고정되어 더이상 바뀌지 않습니다. 

한 단계당 하나의 노드에 대한 최단거리를 확실히 찾는 것으로 이해할 수  있다 

다익스트라 알고리즘을 수행한 뒤에 테이블에 각 노드까지의 최단 거리 정보가 저장 

완벽한 형태의 최단경로를 구하려면 소스코드에 추가적인 기능을 더 넣어야 함 

다익스트라 알고리즘 : 간단한 구현 당법 
단계마다 방문하지 않은 노드 중에서 최단거리가 가장 짧은 노드를 선택하기 위해 매 단계마다 1차원 테이블의 모든 원소를 확인(순차탐색)합니다

import sys
input = sys.stdin.readline
INF = int(1e9)
​
n, m = map(int, input().split())
​
start = int(input())
​
graph = [[]for i in range(n+1)]
​
visited = [False] * (n+1)
distance = [INF]*(n+1)
​
for _ in range(m):
    a,b,c, = map(int, input().split())
    graph[a].append((b,c))
​
def get_smallest_node():
    min_value = INF
    index = 0
    for i in range(1, n+1):
        if distance[i] < min_value and not visited[i]:
            min_value = distance[1]
            index = i
        return index
​
​
def dijkstra(start):
    distance[start] = 0
    visited[start] = True
    for j in graph[start]:
        distance[j[0]] = j[1]
    for i in range(n-1):
        now = get_smallest_node()
        visited[now] = True
​
        for j in graph[now]:
            cost = distance[now]+j[i]
            if cost < distance[j[0]]:
                distance[j[0]]= cost
​
​
dijkstra(start)
​
for i in range(1, n+1):
    if distance[i] == INF:
        print("INFINITY")
    else:
        print(distance[i])
다익스트라 알고리즘 : 간단한 구현 방법 성능 분석 
총 O(V) 번에 걸쳐서 최단거리가 가장 짧은 노드를 매번 선형 탐색해야함 

짜라서 전체 시간 복잡고는 O(V^2)

일반적으로 코테의 최단 경로문제에서 전체 노드 갯수가 5000개 이하라면 이 코드로 문제 해결 가능

하지만 노드 갯수가 10000개 이상이라면? 

우선순위 큐 (Priority Queue)
우선순위가 가장 높은 데이터를 가장 먼저 삭제하는 자료구조

예를 들어 여러개의 물건 데이터를 자료구조에 넣었다가 가치가 높은 물건 데이터부터 꺼내서 확인해야 하는 경우에 우선순위 큐를 이용할 수 있음 

대부분의 프로그래밍 언어에서 표준 라이브러리 형태로 지원 

image-20201118223214492

힙 (Heap)
우선순위 큐를 구현하기 위해 사용하는 자료구조 중 하나 

최소 힙 ( Min Heap) 과 최대 힙 (Max Heap)이 있습니다. 

다익스트라 최단 경로 알고리즘을 포함해 다양한 알고리즘에서 사용 

image-20201118223325269

import heapq
​
def heapsort(iterable):
    h = []
    result = []
    
    for value in iterable:
        heapq.heappush(h, value)
        
    for i in range(len(h)):
        result.append(heapq.heappop(h))
    return result
​
result = heapsort([1,3,5,7,9,2,4,6,8,0])
​
print(result)
다익스트라 알고리즘 : 개선된 구현 방법 
단계마다 방문하지 않은 노드 중에서 최단거리가 가장 짧은 노드를 선택하기 위해 힙 자료구조를 이용

다익스트라 알고리즘이 동작하는 기본원리는 동일 

현재 가장 가까운 노드를 저장해 놓기 위해 힙 자료구조를 추가적으로 이용한다는 점이 다름 

현재의 최단거리가 가장 짧은 노드를 선택해야 하므로 최소 힙을 사용  

다익스트라 알고리즘 : 동작 과정 살펴보기 (우선순위 큐)
image-20201118223801737

image-20201118223825650

image-20201118223839787

![image-20201118223853055](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201118223853055.png)image-20201118223853055

image-20201118223904171

image-20201118223919552

image-20201118223931629

image-20201118223947331

image-20201118223957991

​
import heapq
import sys
​
input = sys.stdin.readline
INF = int(1e9)
​
n, m = map(int, input().split())
​
start = int(input())
​
graph = [[]for i in range(n+1)]
​
visited = [False] * (n+1)
distance = [INF]*(n+1)
​
for _ in range(m):
    a,b,c, = map(int, input().split())
    graph[a].append((b,c))
​
​
​
def dijkstra(start):
    q= []
​
    heapq.heappush(1, (0,start))
    distance[start] = 0
​
    while q:
        dist, now = heapq.heappop(q)
        if distance[now] < dist:
            continue
        for i in graph[now]:
            cost = dist +i[1]
            if cost < distance[i[0]]:
                distance[i[0]] = cost
                heapq.heappush(q, (cost, i[0]))
​
dijkstra(start)
​
for i in range(1, n+1):
    if distance[i]==INF:
        print("INFINITY")
    else:
        print(distance[i])
다익스트라 알고리즘 : 개선된 구현 방법 성능 분석 
힙 자료구조를 이용하는 다익스트라 알고리즘의 시간 복잡도는 O(E*logV)

노드를 하나씩 꺼내 검사하는 반복문 (While문)의 노드의 개수 V이상의 횟수로는 처리되지 않음 

결과적으로 현재 우선순위 큐에서 꺼낸 노드와 연결된 다른 노드들을 확인하는 총 횟수는 최대 간선의 개수(E)만큼 연산이 수행 될 수 있음 

직관적으로 전체 과정은 E개의 원소를 우선순위 큐에 넣었다가 모두 뺴내는 연산과 매우 유사합니다 

시간 복잡도를 O(E*logE)로 판단 가능 

중복 간선을 포함하지 않는 경우에 이를 O(E*logV) 로 정리될 수 있습니다.

O(ElogE)--> O(ElogV^2)-> O(2ElogV) --> O(ElogV)

