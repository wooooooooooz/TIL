# 계수 정렬 

## 특정한 조건의 부합할 때만 사용할 수 있지만 매우 빠르게 동작하는 정렬 알고리즘

- 계수 정렬은 데이터의 크기 범위가 제한되어 정수 형태로 표현할 수 있을때 사용 가능 

## 데이터 개수가 N, 데이터(양수) 중 최대값이 K일때 최악의 경우에도 수행시간 O(N+K)를 보장합니다.  

### Step 0 : 가장 작은 데이터부터 가장 큰 데이터까지의 범위가 모두 담길 수 있도록 리스트 생성 

![image-20201110225638527](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201110225638527.png)

### Step 1 : 데이터를 하나씩 확인하며 데이터의 값과 동일한 인덱스의 데이터를 1씩 증가시킵니다. 

![image-20201110225742759](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201110225742759.png)

### Step 2 :  반복 

### Step 15 : 결과적으로 최종 리스트에는 각 데이터가 몇번씩 등장했는지 그 횟수가 기록됨 

![image-20201110225924750](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201110225924750.png)



### 결과를 확인할 떄는 리스트의 첫 번째 데이터 분터 하나씩 그 값만큼 반복하여 인덱스를 출력 

![image-20201110230055957](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201110230055957.png)

## 계수정렬 소스코드 

```python
# 모든 원소의 값이 0보다 크거나 같다고 가정

array = [7,5,9,0,3,1,6,2,9,1,4,8,0,5,2]

# 모든 범위를 포함하는 리스트 선언 (모든값은 0으로 초기화)
count = [0] * (max(array)+1)

for i in range(len(array)):
    count[array[i]] +=1  # 각 데이터에 해당하는 인덱스 값 증가

for i in range(len(count)):
    for j in range(count[i]):
        print(i, end = " ") # 등장한 횟수만큼 (j번) 인덱스 출력 
```



## 계수 정렬의 복잡도 분석 

- 계수 정렬의 시간 복잡도와 공간 복잡도는 모두 O(N+K)입니다.
- 계수정렬은 떄에 따라서 심각한 비효율 초래 가능 
  - 데이터가 0, 999999 딱 2개 있다면 ? : 길이 10만의 리스트를 만들어야 함 
- 계수 정렬은 동일한 값을 가지는 데이터가 여러 개 등장할 때 효과적으로 사용할 수 있다 
  - 시험성적의 경우 100점이 다수 있을 수 있으니 계수 정렬이 효과적 
