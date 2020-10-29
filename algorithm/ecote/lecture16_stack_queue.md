# 스택과 큐 자료구조 

## 1. 스택 자료구조 

- 먼저 들어온 데이터가 나중에 나간다 (선입후출) 
- 스택은 입구와 출구가 동일한 형태로 시각화 가능 

```python 
list = [] 

stack.append(1)
stack.append(2)
stack.append(3)
stack.append(4)
stack.pop()

stack.append(5)
stack.append(6)
stack.pop()

print(stack[::-1]) 	# 최상단 원소부터 출력 
print(stack) 		# 최하단 원소부터 출력 

```


## 2. 큐 자료구조 

- 먼저 들어온 데이터가 먼저 나간다 (선입선출) 
- 큐는 입구와 출구가 있는 터널 형태로 시각화 가능 

```python 
from collections import deque  
# deque : double ended Queue 를 의미 
# 리스트로 큐를 구현할 수도 있지만, 시간복잡도가 증가한다 

queue = deque()   # 데크 객체 생성 

queue.append(1)
queue.append(2)
queue.append(3)
queue.append(4)

queue.popleft()
queue.append(5)
queue.append(6)

print(queue)    # 먼저 들어온 순서대로 출력 
queue.reverse() # 큐 순서 뒤집기 
print(queue)  # 나중에 들어온 순서대로 출력됨 
```





