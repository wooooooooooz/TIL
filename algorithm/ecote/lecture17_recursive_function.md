# 재귀함수 

## 재귀함수란 자기 자신을 다시 호출하는 함수를 말한다 



###  단순한 형태의 재귀함수 예제 

```python
def recursive_function():
    print("재귀함수를 호출합니다")
    recursive_function()

resursive_function()
```



### 재귀함수의 종료 조건 

- 재귀함수를 문제풀이에 사용할때는 반드시 종료조건을 명시 
- 종료조건을 명시하지 않으면 무한히 호출된다



```python
def recursive_function(i):
    # 100번째 반복에서 종료 
    if i==100:
        return 
    recursive_function(i+1)
    
recursive_function(1)
```





### 팩토리얼 구현 예제

```python
def factorial(n):
    if n =< 1:
        return 1 
    return n*factorial(n-1)
factorial(100)
```



### 최대공약수 구현 예제 (유클리드 호제법)

- 두 자연수 A,B 에 대해 (A>B) A를 B로 나눈 나머지를 R로 하자 
- 이때 A와 B의 최대공약수는 B와 R의 최대공약수와 같다  

```python
def gcd(a,b):
    if a%b == 0:
        return b
    else
    	return gcd(b, a%b)
print(gcd(192,162))
```



## 재귀함수 사용시 유의사항 

- 재귀함수는 잘 사용하는 복잡한 알고리즘 단순화 가능 
  - 단, 다른 사람이 볼때 이해하기 어려워 질 수도 
- 모든 재귀함수는 반복문으로 같은 기능 구현 가능 
  - 재귀함수가 반복문보다 유리할수도 있고 불리할 수도 있다 
- 컴퓨터가 함수를 연속적으로 호출하면 컴퓨터 메모리 내부의 스택 프레임에 쌓입니다 
  - 따라서 스택을 사용해야 할때 구현상 스택 라이브러리 대신 재귀함수를 이용하는 경우가 많다 
