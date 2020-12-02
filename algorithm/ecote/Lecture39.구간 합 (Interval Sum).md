# 구간 합 (Interval Sum)

- __구간 합 문제__ : 연속적으로 나열된 N개의 수가 있을때 특정 구간의 모든 수를 합한 값을 계산하는 문제 
- 예를 들어 5개의 데이터로 구성된 수열 {10,20,30,40,50} 이 있다고 가정 
  - 두 번째 수부터 네 번쨰 수까지의 합은 20 +30 + 40 = 90 



## 구간 합 빠르게 계산하기 : 문제 설명 

- N개의 정수로 구성된 수열이 있습니다. 
- M개의 쿼리 (Query) 정보가 주어집니다. 
  - 각 쿼리는 Left 와 Right 로 구성 
  - 각 쿼리에 대해 [Left, Right] 구간에 포함된 데이터들의 합을 출력해야 함 
- 수행 시간 제한은 O (N + M)

## 구간 합 빠르게 계산하기 : 문제 해결 아이디어 

- __접두사 합(Prefix Sum)__ : 배열의 맨 앞부터 특정 위치까지의 합을 미리 구해 놓은 것 
- 접두사 합을 활용한 알고리즘은 다음과 같습니다. 
  - N개의 수 위치에 각각에 대해 접두사 합을 계산해 P에 저장 
  - 매 M개의 쿼리 정보를 확인 할 때 구간 합은 P[Right] - P[Left-1] 

![image-20201203000342061](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201203000342061.png)

 ## 구간 합 빠르게 계산하기 : 코드 예시 

```python
n = 5
data = [10,20,30,40,50]

sum_value = 0
prefix_sum = [0]

for i in data:
    sum_value += i
    prefix_sum.append(sum_value)
    
left = 3
right = 4
print(prefix_sum[right] - prefix_sum[left-1])

```



