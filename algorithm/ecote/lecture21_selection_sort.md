#  정렬 알고리즘 (1)

- 정렬(Sorting)이란 데이터를 특정한 기준에 따라 순서대로 나열하는 것
- 일반적으로 문제 상황에 따라 적절한 정렬 알고리즘이 공식처럼 사용 

## 0 ~ 9  가 쓰인 카드를 정렬 하는 법?

## 선택정렬 

- 처리되지 않은 데이터 중에서 가장 작은 데이터를 선택해 맨 앞에 있는 데이터와 바꾸는 것을 반복 

  ![image-20201105195258692](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201105195258692.png)

- 처리되지 않은 데이터 중 가장 작은 '1'을 선택해 가장 앞의 '5'와 바꿈 

![image-20201105195340323](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201105195340323.png)

- 이 과정을 반복 



### 선택 정렬 소스코드 

```py
array = [7,5,9,0,3,1,6,2,4,8]

for i in range(len(array)):
	min_index = i
	
	for j in range(i+1, len(array)):
		if array[min_index] > array[j]:
			min_index = j
	array[i], array[min_index] = array[min_index], array[i] # 스왑
print(array)
```

