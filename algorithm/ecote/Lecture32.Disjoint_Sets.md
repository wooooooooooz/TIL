# 기타 그래프 이론 : 서로소 집합 

- 서로소 집합 (Disjoint Sets)란 __공통원소가 없는 두 집합__을 의미합니다

![image-20201123221809836](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201123221809836.png)

## 서로소 집합 자료구조 

- __서로소 부분 집합들로 나누어진 원소들의 데이터를 처리하기 위한 자료구조__
- 서로소 집합 자료구조는 두 종류의 연산을 지원 
  - 합집합(Union) : 두개의 원소가 포함된 집합을 하나의 집합으로 합치는 연산 
  - 찾기 (Find) : 특정한 원소가 속한 집합이 어떤 집합인지 알려주는 연산 
- 서로소 집합 자료구조는 __합치기 찾기 (Union Find) 자료구조__ 라고 불림



- 여러개의 합치기 연산이 주어졌을 때 서로소 집합 자료구조의 동작 과정은 다음과 같다 

  1. 합집합(Union) 연산을 확인하여, 서로 연결된 두 노드 A, B를 확인합니다. 

     1)	A와 B의 루트 노드 A', B' 를 각각 찾음 

     2) 	A', B' 의 부모 노드로 설정 

  2. 모든 합집합(Union) 연산을 처리할 떄까지 1번의 과정을 반복 

## 서로소 집합 자료구조 : 동작 과정 살펴보기 

- 처리할 연산들 : Union(1,4), Union(2,3), Union(2,4), Union(5,6)
- 초기단계 : 노드의 개수 크기의 부모 테이블을 초기화 

![image-20201123222338614](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201123222338614.png)

- [Step 1] 노드 1과 노드 4의 루트 노드를 각각 찾습니다. 현재 루트 노드는 각각 1과 4이므로 더 큰 번호에 해당하는 루트노드 4의 부모를 1로 설정 

![image-20201123222445782](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201123222445782.png)

- [Step 2] 노드 2와 노드 3의 루트노드를 각각 찾습니다. 현재 루트 노드는 각각 2와 3이므로 더 큰 번호에 해당하는 루트 노드 3의 부모를 2로 설정합니다.  

![image-20201123222539356](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201123222539356.png)

- [Step 3] 노드2와 노드 4의 루트노드를 각각 찾습니다. 현재 루트 노드는 각각 2와 1이므로 더 큰 번호에 해당하는 루트노드 2의 부모를 1로 설정합니다. 

![image-20201123222651497](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201123222651497.png)

- [Step 4] 노드 5와 노드 6의 루트 노드를 각각 찾습니다. 현재 루트 노드는 각각 5와 6이므로 더 큰 번호에 해당하는 루트 노드6의 부모를 5로 설정합니다. 

![image-20201123222757880](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201123222757880.png)

### 서로소 집합 자료구조 : 연결성 

- 서로소 집합 자료구조에서는 __연결성__을 통해 손쉽게 집합의 형태를 확인 

![image-20201123222849845](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201123222849845.png)

- 기본적인 형태의 서로소 집합 자료구조에서는 루트노드에 즉시 접근 불가. 
  - 루트 노드를 찾기위해 부모 테이블을 계속해서 확인하며 거슬러 올라가야 함 
- 다음 예시에서 노드 3의 루트를 찾기 위해서는 노드2를 거쳐 노드1에 접근해야 함 

![image-20201123223033524](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201123223033524.png)



```python
def find_parent(parent, x):
    if parent[x] != x:
        return parent[x] = find_parent(parent, parent[x])
    return x
def union_parent(parent, a, b):
    a = find_parent(parent, a)
    b = find_parent(parent, b)
    if a < b:
        parent[b] = a
    else: 
        parent[a] = b

# 노드 갯수와 간선 (Union 연산)의 갯수 입력 받기 
v,e = map(int, input().split())
parent = [0] * (v + 1)

for i in range(1, v+1):
    parent[i] = i
    
for i in range(e):
    a,b = map(int, input().split())
    union_parent(parent, a, b)
print('각 원소가 속한 집합 :' , end = '')
for i in range(1, v+1):
    print(find_parent(parent, i), end = ' ')
print()

print('부모 테이블: ', end ='')
for i in range(1, v+1):
    print(parent[i], end = ' ')
```



## 서로소 집합 자료구조 : 기본적인 구현 방법의 문제점 

- 합집합(Union) 연산이 편향되게 이루어지는 경우 찾기(Find) 함수가 비효율 적으로 동작 

- 최악의 경우에는 찾기(Find) 함수가 모든 노드를 다 확인하게 되어 시간복잡도가 O(V)이다 

  - 다음과 같이 {1,2,3,4,5} 총 5개의 원소가 존재하는 상황 확인 
  - __수행된 연산들__ : Union(4,5) , Union(3,4), Union(2,3), Union(1,2)

  ![image-20201123223443157](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201123223443157.png)

### 서로소 집합 자료구조 : 경로 압축 

- 찾기 (Find) 함수를 최적화하기 위한 방법으로 경로 압축 (Path Compression)을 이용할 수 있습니다.

  - 찾기(FInd) 함수를 재귀적으로 호출한 뒤에 __부모 테이블 값을 바로 갱신__ 합니다. 

  - ```python
    def find_parent(parent, x):
        if parent[x] != x:
            parent[x] = find_parent(parent, parent[x])
            return parent[x]
    ```

- 경로 압축 기법을 적용하면 각 노드에 대하여 찾기(Find) 함수를 호출한 이후에 해당 노드의 루트노드가 바로 부모 노드가 됨 
- 동일한 예시에 대해 __모든 합집합(Union) 함수를 처리한 후 각 원소에 대해 찾기(Find) 함수를 수행하면 다음과 같이 부모 테이블이 갱신__
- 기본적인 방법에 비해 시간 복잡도 개선 

![image-20201123223916822](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201123223916822.png)

```python
def find_parent(parent, x):
    if parent[x] != x:
        parent[x] = find_parent(parent, parent[x])
        return parent[x]
def union_parent(parent, a, b):
    a = find_parent(parent, a)
    b = find_parent(parent, b)
    if a < b:
        parent[b] = a
    else: 
        parent[a] = b
        
v,e = map(int, input().split())
parent = [0] * (v + 1)

for i in range(1, v+1):
    parent[i] = i
    
for i in range(e):
    a,b = map(int, input().split())
    union_parent(parent, a, b)
print('각 원소가 속한 집합 :' , end = '')
for i in range(1, v+1):
    print(find_parent(parent, i), end = ' ')
print()

print('부모 테이블: ', end ='')
for i in range(1, v+1):
    print(parent[i], end = ' ')
```







