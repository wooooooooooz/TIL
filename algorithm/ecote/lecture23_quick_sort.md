# 퀵 정렬 

## 기준 데이터를 설정하고 그 기준보다 큰 데이터와 작은 데이터의 위치를 바꾸는 방법 

- 일반적인 상황에서 가장 많이 사용되는 정렬 알고리즘 
- 병합 정렬과 더불어 대부분의 프로그래밍 언어의 정렬 라이브러리의 근간이 되는 알고리즘 
- 가장 기본적인 퀵 정렬은 첫번째 데이터를 기준 데이터(Pivot)로 설정한다 

### 퀵 정렬 동작 예시 

- Step 0 : 현재 피벗의 값은 5이다. 왼쪽에서부터 5보다 큰 데이터를 선택하므로 7이 선택되고, 오른쪽에서 5보다 작은 데이터를 선택하므로 4가 선택된다.  이제 이 두 데이터의 위치를 서로 변경한다. 

![image-20201109212714373](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201109212714373.png)

- Step 1 : 현재 피벗의 값은 5이다. 왼쪽에서 부터 5 보다 큰 데이터를 선택하므로 9가 선택되고, 오른쪽에서 부터 5보다 작은 데이터를 선택하므로 2가 선택됩니다. 이제 이 두 데이터의 위치를 변경한다.

![image-20201109212729049](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201109212729049.png)



- Step 2: 현재 피벗 값은 5이다. 왼쪽에서부터 5보다 큰 데이터를 선택하므로 6이 선택되고, 오른쪽에서부터 5보다 작은 데이터를 선택하므로 1이 선택된다. 단 이처럼 위치가 엇갈리는 경우 ''피벗''과 ''작은 데이터''의 위치를 서로 변경한다. 

![image-20201109212855127](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201109212855127.png)

- 분할 완료 : 이제 '5'의 왼쪽에 있는 데이터는 모두 5보다 작고, 오른쪽에 있는 데이터는 모두 5보다 크다는 특징이 있다. 이렇게 피벗을 기준으로 데이터 묶음을 나누는 작업을 분할(Divide)라고 한다.  

![image-20201109213356164](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201109213356164.png)



- 왼쪽 데이터 묶음 정렬 : 왼쪽에 있는 데이터에 대해 마찬가지로 정렬 수행 

![image-20201109214137335](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201109214137335.png)



### 퀵 정렬이 빠른 이유 : 직관적인 이해 

-  이상적인 경우 분할이 절반씩 일어난다면 전체 연산 횟수로 O(N*logN)을 기대 
  - 너비 * 높이 = N * logN  

![image-20201109214341583](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201109214341583.png)



### 퀵 정렬의 시간 복잡도 

- 퀵 정렬은 평균의 경우 O(N*logN)

- 최악의 경우 O(N^2)의 시간복잡도를 가짐 

  - 첫 번째 원소를 피벗으로 삼을때, 이미 정렬된 배열에 대해 퀵 정렬을 수행하면? 

- ![image-20201109214610845](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201109214610845.png)

  

### 퀵 정렬 소스코드 

```python
array = [5,7,9,0,3,1,6,2,4,8]

def quick_sort(array, start, end):
    if start >= end:
        return

    pivot = start
    left = start +1
    right = end

    while(left <= right):

        while(left <= end and array[left] <= array[pivot]):
            left += 1
        while(right > start and array[right] >= array[pivot]):
            right -= 1
        if (left > right):
            array[right], array[pivot] = array[pivot], array[right]
        else:
            array[left], array[pivot] = array[left], array[right]

    quick_sort(array, start, right -1)
    quick_sort(array, right+1, end )

quick_sort(array,  0 ,len(array)-1)
print(array)
```



### 파이써닉한 방법 

```python
array = [5,7,9,0,3,1,6,2,4,8]

def quick_sort(array):
    if len(array) <= 1:
        return array

    pivot = array[0]
    tail  = array[1:] # 피벗을 제외한 리스트

    left_side = [x for x in tail if x <= pivot]
    right_side = [x for x in tail if x > pivot]

    # 분할 이후 왼쪽 부분과 오른쪽 부분에서 각각 정렬 수행하고, 전체 리스트 반환

    return quick_sort(left_side) + [pivot] + quick_sort(right_side)
print(quick_sort(array))

```

