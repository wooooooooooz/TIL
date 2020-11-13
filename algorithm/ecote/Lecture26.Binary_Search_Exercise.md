# 이진 탐색 문제 기초 풀이 

## <문제> 떡볶이 떡 만들기 : 문제 설명 

-  동빈이네 떡볶이 떡은 떡의 길이가 일정하지 않다. 대신 한 봉지 안에 들어가는 떡의 총 길이는 절단기로 잘라서 맞춰줍니다. 
-  절단기에 __높이(H)__ 를 지정하면 줄지어진 떡을 한번에 절단합니다. 높이가 H보다 긴 떡은 H 위의 부분이 잘릴 것이고, 낮은 떡은 잘리지 않는다. 
-  예) 높이가 19, 14, 10 17cm 인 떡이 나란히 있고 절단기 높이를 15cm로 지정하면 자른 뒤 떡의 높이는 15, 14, 10, 15cm 가 될 것이다. 잘린 떡의 길이는 차례대로 4,0,0,2cm 입니다. 손님은 6cm 를 가져간다. 
-  손님이 왔을 때 요청한 총 길이가 M일 때 __적어도 M 만큼의 떡을 얻기 위해 절단기에 설정할 수 있는 높이의 최댓값을 구하는 프로그램__을 작성 

## 문제 조건 

![image-20201113191335175](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201113191335175.png)

## 문제 해결 아이디어

- 적절한 높이를 찾을 때까지 이진 탐색을 수행하여 높이 H를 반복해서 조정
- '현재 이 높이로 자르면 조건을 만족할 수 있는가?'를 확인 후 __조건의 만족 여부('Yes or No') 에 따라서 탐색 범위를 좁혀서 해결__
- 절단기의 높이는 0 ~ 10억 까지의 정수 중 하나 
  - 이렇게 __큰 탐색 범위__를 보면 가장 먼저 __이진 탐색__을 떠올려야 함 

### Step 1 : 시작점 : 0, 끝점 : 19, 중간점 : 9   (이때 필요한 떡의 크기 : M = 6이므로, 결과 저장 )

###  ![image-20201113191738401](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201113191738401.png)

### Step 2: 시작점 : 10, 끝점 : 19, 중간점: 14    (이때 필요한 떡의 크기 : M = 6이므로, 결과 저장 )

![image-20201113191844823](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201113191844823.png)

### Step 3 : 시작점 : 15, 끝점: 19, 중간점 : 17  (이때 필요한 떡의 크기 : M = 6이므로, 결과 저장 )

![image-20201113191920913](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201113191920913.png)

## Step 4 : 시작점 : 15, 끝점: 16, 중간점 : 15  (이때 필요한 떡의 크기 : M = 6이므로, 결과 저장 )

![image-20201113191950690](C:\Users\scoji\TIL\image-20201113191950690.png)

### 이러한 이진 탐색을 반복하면 답을 도출 가능 

### 중간점의 값을 __시간이 지날수록 '최적화된 값'__이 되기 때문에, 과정을 반복하면서 얻을 수 있는 떡의 길이 합이 필요한 떡의 길이보다 크거나 같을 때마다 __중간점의 값을 기록__하면 됩니다. 

## 답안 예시 (Python)

```python
# 떡의 갯수 (N)과 요청한 떡의 길이(M)을 입력
n, m = list(map(int, input().split(' ')))

# 각 떡의 개별 높이 정보를 입력
array = list(map(int, input().split()))

# 이진 탐색을 위한 시작점과 끝점 설정
start = 0
end = max(array)

# 이진 탐색 수행
result = 0
while(start <= end):
    total = 0
    mid = (start+end) //2
    for x in array:
        if x > mid:
            total += x - mid
        if total < m:
            end = mid -1
        else:
            result = mid
            start = mid+1
print(result)
```



## 정렬된 배열에서 특정 수의 갯수 구하기 : 문제설명 

-  N개의 원소를 포함하고 있는 수열이 오름차순으로 정렬되어 있다. 이때 이 수열에서 x가 등장하는 횟수를 계산하세요. 예를 들어 수열 {1,1,2,2,2,2,3}이 있을 때 x = 2라면, 현재 수열에서 값이 2인 원소가 4개이므로 4를 출력합니다. 
-  단, 이 문제는 시간 복잡도 O(logN)으로 알고리즘을 설계하지 않으면 __시간 초과__ 판정을 받습니다.  

![image-20201113192900616](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201113192900616.png)

### 문제 해결 아이디어 

- 시간 복잡도 O(logN)으로 동작하는 알고리즘을 요구 
  - 일반적인 선형 탐색으로는 시간 초과 판정을 받습니다. 
  - 하지만 데이터가 정렬되어 있기 때문에 이진 탐색을 수행할 수 있습니다. 
- 특정 값이 등장하는 첫 번째 위치와 마지막 위치를 찾아 위치 차이를 계산해 문제를 해결할 수 있습니다.

![image-20201113193046278](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201113193046278.png)

### 답안 예시 

```python
# 떡의 갯수 (N)과 요청한 떡의 길이(M)을 입력
n, m = list(map(int, input().split(' ')))

# 각 떡의 개별 높이 정보를 입력
array = list(map(int, input().split()))

# 이진 탐색을 위한 시작점과 끝점 설정
start = 0
end = max(array)

# 이진 탐색 수행
result = 0
while(start <= end):
    total = 0
    mid = (start+end) //2
    for x in array:
        if x > mid:
            total += x - mid
        if total < m:
            end = mid -1
        else:
            result = mid
            start = mid+1
print(result)


##################

from bisect import bisect_left, bisect_right

def count_by_range(a, left_value, right_value):
    right_index = bisect_right(a, right_value)
    left_index = bisect_left(a, left_value)
    return right_index - left_index

# 떡의 갯수 (N)과 요청한 떡의 길이(M)을 입력
n, x = map(int, input().split())
array = list(map(int, input().split()))

count = count_by_range(array, x,x)

if count == 0:
    print(-1)
else:
    print(count)
```



