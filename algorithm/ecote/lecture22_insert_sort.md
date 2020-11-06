# 정렬 알고리즘 (2)

## 삽입 정렬 

- 처리되지 않은 데이터를 하나씩 골라 적절한 위치에 삽입 
- 선택 정렬에 비해 구현 난이도가 높지만, 일반적으로 더 효율적으로 동작 

### 삽입 정렬 동작 예시 

- Step0 : 첫 번째 데이터 7은 그 자체로 정렬이 되어 있다고 판단하고, 두 번째 데이터인 5가 어떤 위치로 들어갈지 판단. 7의 왼쪽으로 들어가거나 오른쪽으로 들어가거나 두 경우만 존재

![image-20201106200214748](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201106200214748.png)

- Step1 : 이어서 9가 어디로 갈지 판단

![image-20201106200418705](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201106200418705.png)

- Step2 : 이어서 0이 어떤 위치로 들어갈지 판단 

![image-20201106200505310](C:\Users\scoji\TIL\image-20201106200505310.png)

- Step3 : 끝까지 반복 

### 삽입 정렬 소스코드 

```python
array = [7,5,9,0,3,1,6,2,4,8]

for i in range(1, len(array)):
    for j in range(i, 0, -1):
        if array[j]< array[j-1]:
            array[j], array[j-1] = array[j-1], array[j]
        else:
            break  # 자기보다 작은 데이터를 만나면 스톱 
print(array)
```



## 삽입 정렬의 시간복잡도 

- 삽입 정렬의 시간 복잡도는 O(N^2)이며, 선택 정렬과 마찬가지로 반복문이 두번 중첩되어 사용 (but 이중 반복문이 쓰인다고 해서 무조건 N^2 은 아님 !)
- 삽입 정렬은 현재 리스트의 데이터가 거의 정렬되어 있는 상태라면 매우 빠르게 동작 
  - 최선의 경우 (이미 정렬된 상태)라면 O(N)의 시간 복잡도를 가짐 
