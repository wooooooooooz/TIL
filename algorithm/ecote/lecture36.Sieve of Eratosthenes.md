# 다수의 소수 판별

- 하나의 수에 대해서 소수인지 아닌지 판별하는 방법을 알아보았습니다.
- 하지만 __특정한 수의 범위 안에 존재하는 모든 소수__ 를 찾아야 할 떄는 어떻게 할까요?
  - __에라토스테네스의 체 알고리즘__을 사용할 수 있다



## 에라토스테네스의 체 알고리즘

- 다수의 자연수에 대해 소수 여부를 판별할 때 사용하는 대표적인 알고리즘 
- 에라토스테네스의 체는 N보다 작거나 같은 모든 소수를 찾을 때 사용 가능 
- 에라토스테네스의 체 알고리즘의 __구체적인 동작 과정__은 다음과 같다
  - 1. 2부터 N까지의 모든 자연수를 나열한다
    2. 남은 수 중에서 아직 처리하지 않은 가장 작은 수 i를 찾는다
    3. 남은 수 중에서 i의 배수를 모두 제거한다. (i는 제거하지 않음)
    4. 더 이상 반복할 수 없을 떄까지 2번과 3번의 과정을 반복 
- [초기 단계] 2부터 26까지의 모든 자연수를 나열한다 (N = 26)

![image-20201130091751219](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201130091751219.png)

[Step 1] 아직 처리하지 않은 가장 작은 수 2를 제외한 2의 배수는 모두 제거합니다. 

![image-20201130091831739](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201130091831739.png)

[Step 2] 아직 처리하지 않은 가장 작은 수 3를 제외한 3의 배수는 모두 제거합니다. 

[Step 3] 아직 처리하지 않은 가장 작은 수 5를 제외한 5의 배수는 모두 제거합니다. ![image-20201130091958348](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201130091958348.png)

- [Step 4] 마찬가지의 과정을 반복했을 때 최종적인 결과이다 

![image-20201130091920717](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201130091920717.png)

```python
import math

n = 1000
array = [True for i in range(n+1)]


for i in rnage(2, int(math.sqrt(n)) + 1):
    if array[i] == True
    	j = 2
        while i * j <= n:
            array[i*j] = False
            j += 1 
for i in range(2, n+1):
    if array[i]:
        print(i, end = '')
```

## 에라토스테네스의 체 알고리즘 성능분석 

- 에라토스테네스의 체 알고리즘의 시간 복잡도는 사실상 선형 시간에 가까울 정도로 매우 빠름 
  - 시간 복잡도는 O(NloglogN)
- 에라토스테네스의 체 알고리즘은 다수의 소수를 찾아야 하는 문제에서 효과적으로 사용 가능 
  - 하지만 각 자연수에 대한 소수 여부를 저장해야 하므로 __메모리가 많이 필요__
  - 10억이 소수인지 아닌지 판별해야 할 때 에라토스테네스의 체를 사용할 수 있을까요? 





