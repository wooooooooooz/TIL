# 스택과 큐 자료구조 

## 1. 스택 자료구조 

- 먼저 들어온 데이터가 나중에 나간다 (선입후출) 
- 입구와 출구가 동일한 형태로 스택 시각화 가능 

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


