# 소수 판별 알고리즘 

## 소수 (Prime Number)

- __소수__란 1보다 큰 자연수 중에서 1과 자기 자신을 제외한 자연수로는 나누어떨어지지 않는 자연수입니다. 
  - 6은 1,2,3,6으로 나누어 떨어지므로 소수가 아닙니다 
  - 7은 1과 7을 제외하고는 나누어 떨어지지 않으므로 소수입니다.
- 코딩 테스트에서는 어떠한 자연수가 소수인지 아닌지 판별해야 하는 문제가 자주 출제 

### 소수의 판별 : 기본적인 알고리즘 

```python
def is_prime_number(x):
    for i in range(2, x):
        if x % i == 0:
            return False 
    return True

print(is_prime_number(4))
print(is_prime_number(7))
```

### 소수의 판별 : 기본적인 알고리즘 성능 분석 

- 2부터 X-1 까지의 모든 자연수에 대하여 연산을 수행해야 합니다.
  - 모든 수를 하나씩 확인 한다는 점에서 시간 복잡도는 O(X)입니다. 

### 약수의 성질 

- __모든 약수가 가운데 약수를 기준으로 곱셈 연산에 대해 대칭__

  - 예를 들어 16의 양수는 1,2,4,8,16 
  - 이때 2 X 8 = 16은  8 X 2 = 16과 대칭입니다. 

- 따라서 우리는 특정한 자연수의 모든 약수를 찾을 때 __가운데 약수(제곱근)__ 까지만 확인 하면 됨 

  - 예를 들어 16이 2로 나누어 떨어진 다는 것은 8로도 나누어 떨어진 다는 것을 의미 

    

## 소수의 판별 : 개선된 알고리즘 

```python
import math

def is_prime_number(x):
    for i in range(2, int(math.sqrt(x))+1):
        if x% i == 0:
            return False
        return True
    
print(is_prime_number(4))
print(is_prime_number(7))
```



## 소수의 판별 : 개선된 알고리즘 성능 분석 

-  2부터 X의 제곱근 (소수점 이하 무시) 까지의 모든 자연수에 대해 연산을 수행해야 함 
  - 시간 복잡도는 O(N<sup>1/2</sup>)