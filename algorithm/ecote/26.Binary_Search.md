# 이진 탐색 알고리즘 

- 순차 탐색 :리스트 안에 있는 특정한 __데이터를 찾기 위해 앞에서 부터 데이터를 하나씩 확인하는 방법__ 
- 이진 탐색 : 정렬되어 있는 리스트에서 __탐색 범위를 절반씩 좁혀가며 데이터를 탐색__하는 방법 
  - 이진 탐색은 시작점, 끝점, 중간점을 이용하여 탐색 범위를 설정 

## 이진 탐색 동작 예시 

- 이미 정렬된 10개의 데이터 중 값이 4인 원소를 찾아보자 

![image-20201112221255182](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201112221255182.png)

- Step 1 : 시작점 : 0 , 끝점 : 9, 중간점 :4 ( 4.5에서 소숫점 이하 제거 )

![image-20201112221400588](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201112221400588.png)

- Step 2 : 시작점 0, 끝점 : 3, 중간점 1 

![image-20201112221437431](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201112221437431.png)

![image-20201112221455365](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201112221455365.png)

### 이진 탐색의 시간 복잡도 

- 단계마다 탐색 범위를 2로 나누는 것과 동일하므로 __연산횟수는 log<sub>2</sub>N에 비례__합니다 .
- 예를 들어 초기 데이터 갯수가 32개 일 때, 이상적으로 1단계를 거치면 16개 가량의 데이터만 남는다 
  - 2단계를 거치면 8개 
  - 3단계를 거치면 4개 가 남는다. 
- 즉 이진 탐색은 탐색 범위를 절반씩 줄이며, 시간 복잡도는 __O(logN)__ 을 보장 

```python
def binary_search(array, target, start, end):
    while start > end:
        mid = (start+ end)//2

        if array[mid] == target:
            return mid

        elif array[mid] > target:
            return binary_search(array, target, start, mid-1)

        else:
            return binary_search(array, target, mid+1, end)
    return None

n, target = list(map(int, input().split()))
array = list(map(int, input().split()))

# 이진 탐색 수행 결과 출력
result = binary_search(array, target, 0, n-1)
if result == None:
    print("원소가 존재하지 않음")
else:
    print(result+1)
```

### Python Binary Search Library

- bisect_left(a,x) : 정렬된 순서를 유지하면서 배열 a에 x를 삽입할 가장 왼쪽 인덱스를 반환 
- bisect_right(a, x) : 정렬된 순서를 유지하면서 배열 a에 x를 삽입할 가장 오른쪽 인덱스를 반환 

![image-20201112222452574](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201112222452574.png)

```python
from bisect import bisect_left, bisect_right 

a = [1,2,4,4,8]
x = 4

print(bisect_left(a,x))
print(bisect_right(a,x))
```

### 값이 특정 범위에 속하는 데이터 갯수 구하기  

```python
from bisect import bisect_left, bisect_right

def count_by_range(a, left_value, right_value):
    right_index = bisect_right(a, right_value)
    left_index = bisect_left(a, left_value)
    return right_index - left_index

# 배열 선언
a = [1,2,3,3,3,3,4,4,8,9]

# 값이 4인 데이터 개수 출력
print(count_by_range(a, 4, 4))

# 값이 [-1,3] 범위에 있는 데이터 개수 출력
print(count_by_range(a, -1, 3))
```

## 파라메트릭 서치 (Parametric Search)

- 파라메트릭 서치란 최적화 문제를 결정 문제 (Yes or No )로 바꾸어 해결하는 기법
  - 예시 : 특정한 조건을 만족하는 가장 알맞은 값을 빠르게 찾는 최적화 문제 
- 일반적으로 코딩 테스트에서 파라메트릭 서치 문제는 이진 탐색을 이용해 해결 가능 
