# 서로소 집합을 활용한 사이클 판별 

- 서로소 집합은 __무방향 그래프 내에서의 사이클을 판별__할때 사용할 수 있다.

  - 참고로 방향 그래프에서의 사이클 여부는 DFS를 이용해 판별 가능 

- __사이클 반별 알고리즘__은 다음과 같다 

  - 1. 각 간선을 하나씩 확인하며 두 노드의 루트 노드를 확인합니다. 

       1) 루트 노드가 서로 다르다면 두 노드에 대해 합집합 (Union) 연산을 수행 

       2) 루트 노드가 서로 같다면 사이클 (Cycle) 이 발생한 것

  - 2. 그래프에 포함되어 있는 모든 간선에 대해 1번 과정을 반복 

## 서로소 집합을 활용한 사이클 판별 : 동작 과정 살펴보기 

- [초기 단계] 모든 노드에 대해 자기 자신을 부모로 설정하는 형태로 부모 테이블 초기화 

![image-20201124154052119](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201124154052119.png)

- [Step 1] 간선 (1,2)를 확인합니다. 노드 1과 노드 2의 루트노드는 각각 1과 2입니다. 따라서 더 큰 번호에 해당하는 노드2의 부모 노드를 1로 변경합니다.

![image-20201124154142929](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201124154142929.png)

[Step 2] 간선 (1,3)를 확인합니다. 노드 1과 노드 3의 루트 노드는 각각 1과 3입니다. 따라서 더 큰 번호에 해당하는 노드3의 부모 노드를 1로 변경합니다.

![image-20201124154219418](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201124154219418.png)

[Step 3] 간선 (2,3)를 확인합니다. 이미 노드 2과 노드 3의 루트노드는 모두 1입니다. 다시 말해 __사이클이 발생__한다는 것을 알 수 있습니다. 

![image-20201124154302992](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201124154302992.png)



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
        
        
# 노드 갯수와 간선 (Union 연산)의 갯수 입력 받기 
v,e = map(int, input().split())
parent = [0] * (v + 1)

for i in range(1, v+1):
    parent[i] = i

cycle = False # 사이클 발생 여부    
 
for i in range(e):
    a,b = map(int, input().split())
    # 사이클이 발생한 경우 종료
	if find_parent(parent, a ) == find_parent(parent,b):
        cycle = True
        break
     else:
        union_parent(parent, a, b)
if cycle:
    print("사이클이 발생했습니다")
else:
    print("사이클이 발생하지 않았습니다.")
```

