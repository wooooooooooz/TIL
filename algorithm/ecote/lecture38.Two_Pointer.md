# 투 포인터 

- 투 포인터 알고리즘은 __리스트에 순차적으로 접근해야 할 때 두개의 점의 위치를 긹하면서 처리__하는 알고리즘을 의미함
- 흔히 2,3,4,5,6,7번 학생을 지목해야 할 때 간단히 '2번 부터 7번 까지의 학생'이라고 부르곤 합니다.
- 리스트에 담신 데이터에 순차적으로 접근해야 할 때는 __시작점__과 __끝점__ 2개의 점으로 접근할 데이터의 범위를 표현할 수 있습니다. 

## 특정한 합을 가지는 부분 연속 수열 찾기 : 문제 설명 

- N개의 자연수로 구성된 수열이 있음 
- __합이 M인 부분 연속 수열의 개수__를 구해보세요 
- 수행 시간 제한은 O (N) 입니다

![image-20201201192901707](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201201192901707.png)

## 특정한 합을 가지는 부분 연속 수열 찾기 : 문제해결 아이디어 

- __투 포인터__를 활용하여 다음과 같은 알고리즘으로 문제를 해결 가능 
  - 1. 시작점과 끝점이 첫 번째 원소의 인덱스(0)를 가리키도록 한다 
    2. 현재 부분 합이 M과 같다면 카운트 한다 
    3. 현재 부분 합이 M보다 작다면, end를 1 증가시킨다 
    4. 현재 부분 합이 M보다 크거나 같다면, start를 1 증가 
    5. 모든 경우를 확인할 때까지 2번 부터 4번 까지의 과정을 반복 
  - ![image-20201201193101641](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201201193101641.png)

- M = 5 
- [초기단계] 시작점과 끝점이 첫 번째 원소의 인데스를 가리키도록 함 
  - 현재의 부분합은 1이므로 무시
  - __현재 카운트__ : 0 
- ![image-20201201193202952](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201201193202952.png)
- [Step 1] 이전 단계에서의 부분합이 1이었기 때문에 end를 1 증가 
  - 현재의 부분합은 3이므로 무시
  - __현재 카운트__ : 0 

![image-20201201193254955](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201201193254955.png)

[Step 2] 이전 단계에서의 부분합이 3이었기 때문에 end를 1 증가 

- 현재의 부분합은 6이므로 무시
- __현재 카운트__ : 0 

[Step 3] 이전 단계에서의 부분합이 6이었기 때문에 start를 1 증가 

- 현재의 부분합은 5이므로 카운트를 증가 
- __현재 카운트__ : 1

![image-20201201193352124](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201201193352124.png)

[Step 4] 이전 단계에서의 부분합이 5이었기 때문에 start를 1 증가 

- 현재의 부분합은 3이므로 무시 
- __현재 카운트__ : 1

![image-20201201193427157](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201201193427157.png)

[Step 5] 이전 단계에서의 부분합이 3이었기 때문에 end를 1 증가 

- 현재의 부분합은 5이므로 카운트를 증가  
- __현재 카운트__ : 2

![image-20201201193508463](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201201193508463.png)

[Step 6] 이전 단계에서의 부분합이 5이었기 때문에 start를 1 증가 

- 현재의 부분합은 2이므로 무시  
- __현재 카운트__ : 2

![image-20201201193539930](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201201193539930.png)

[Step 7] 이전 단계에서의 부분합이 2이었기 때문에 end를 1 증가 

- 현재의 부분합은 7이므로 무시  
- __현재 카운트__ : 2

![image-20201201193609873](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201201193609873.png)

[Step 8] 이전 단계에서의 부분합이 7이었기 때문에 start를 1 증가 

- 현재의 부분합은 5이므로 카운트를 증가   
- __현재 카운트__ : 3

## 특정한 합을 가지는 부분 연속 수열 찾기 

```python
n = 5
m = 5 
data = [1,2,3,4,5]

count = 0
interval_sum = 0
end = 0

for start in range(n):
    while interval_sum < m and end < n:
		interval_sum += data[end]
        end += 1
    if interval_sum == m:
        count += 1
    interval_sum -= data[start]
 print(count)
```

