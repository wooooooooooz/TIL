# 다이나믹 프로그래밍 문제 풀이 

## <문제> 개미 전사 : 문제 설명 

- 개미 전사는 부족한 식량을 충당하고자 메뚜기 마을의 식량창고를 공격한다. 식량창고는 일직선으로 이어져있다. 
- 각 식량창고에는 정해진 수의 식량을 저장하고 있으며 개미 전사는 식량창고를 선택적으로 약탈할 예정. 메뚜기는 일직선상에 존재하는 식량창고 중에서 서로 인접한 식량창고가 공격받으면 바로 알아챌 수 있다. 
- 따라서 개미 전사가 안들키고 약탈하기 위해서는 __최소한 한 칸 이상 떨어진 식량창고를 약탈__해야 합니다. 

![image-20201117221526495](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201117221526495.png)

- 예를 들어 식량창고 4개가 다음과 같이 존재한다. 
  - {1,3,1,5}
- 개미는 두번쨰 식량창고와 네번째 식량창고를 선택했을 떄 최댓값인 총 8개의 식량을 뺏을 수 있다. 개미는 일직선상일때 최대한 많은 식량을 얻기를 원합니다. 
- 개미 전사를 위해 식량창고 N개에 대한 정보가 주어졌을 때 __얻을 수 있는 식량의 최댓값__을 구하는 프로그램 작성 

![image-20201117221754196](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201117221754196.png)

- 예시 : N  = 4일때 다음과 같은 경우가 존재.
  - 식량을 선택할 수 있는 경우는 8가지
  - 7번쨰 경우에서 8만큼의 식량을 얻는 것이 최적해 
- ![image-20201117221853141](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201117221853141.png)



- a<sub>i</sub> = i 번째 식량창고까지의 최적 해 (얻을 수 있는 식량의 최댓값)
  - 이렇게 정의한다면 다이나믹 프로그래밍을 적용할 수 있다, 

![image-20201117222002545](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201117222002545.png)

- 왼쪽부터 차례대로 창고를 턴다고 했을때, 특정한 i번쨰 식량창고에 대해 털지 안털지의 여부를 결정하면, 아래 2가지 경우 중에서 더 많은 식량을 털 수 있는 경우를 선택하면 됩니다. 

![image-20201117222114585](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201117222114585.png)

- a<sub>i</sub> = i 번째 식량창고까지의 최적 해 (얻을 수 있는 식량의 최댓값)
- k<sub>i</sub> = i 번째 식량창고에 있는 식량의 양 
- 점화식은 다음과 같다 
  - a<sub>i</sub>	=  max(a<sub>i-1</sub> , a<sub>i-2</sub> + k<sub>i</sub>)		
- 한 칸 이상 떨어진 식량창고는 항상 털 수 있으므로 (i-3)번째 이하는 고려할 필요가 없다 

### 답안 예시 

```python
n = int(input())

array = list(map(int, input().split()))
d[0] *100

d[0] = array[0]
d[1] = max(array[0], array[1])
for i in range(2,n):
    d[i] = max(d[i-1], d[i-2]+array[i])

print(d[n-1])
```



## <문제> 1로 만들기 : 문제 설명 

- 정수 X가 주어졌을 때, 정수 X에 사용할 수 있는 연산은 4가지 
  1. X가 5로 나누어 떨어지면, 5로 나눈다. 
  2. X가 3으로 나누어 떨어지면, 3로 나눈다. 
  3. X가 2로 나누어 떨어지면, 2로 나눈다. 
  4. X에서 1을 뺍니다. 
- 정수 X가 주어졌을 때, 연산 4개를 적절히 사용해서 값을 1로 만들고자 한다. 연산을 사용하는 횟수의 최솟값을 출력하세요. 예를 들어 정수가 26이면 3번의 연산이 최솟값입니다. 
  -  26 -> 25 -> 5 -> 1 

### 문제해결 아이디어 

- 피보나치 수열 문제를 도식화한 것처럼 함수가 호출되는 과정을 그려보자 
  - __최적 부분 구조와 중복되는 부분 문제__를 만족합니다. 
- ![image-20201117223110425](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201117223110425.png)



- a<sub>i</sub> = i 를 1로 만들기 위한 최소 연산 횟수 
- 점화식
  - a<sub>i</sub> = min ( a<sub>i-1</sub>, a<sub>i/2</sub>, a<sub>i/3</sub>, a<sub>i/5</sub>) + 1 
- 단, 1을 뺴는 연산을 제외하고는 __해당 수로 나누어 쩔어질때만 점화식 적용__할 수 있다

### 1로 만들기 : 답안 예시 

```python
x = int(input())

d = [0] * 3001

for i in range(2, x+1):
    d[i] = d[i-1] +1
    
    if i%2 ==0:
        d[i] = min(d[i], d[i//2] +1)
	if i%3 ==0:
        d[i] = min(d[i], d[i//3] +1)
	if i%5 ==0:
        d[i] = min(d[i], d[i//5] +1)
print(d[x])
```



## 효율적인 화폐 구성 : 문제 설명 

- N가지 종류 화폐가 있다. 이 화폐들의 개수를 최소한으로 이용해서 그 가치의 합이 M 원이 되도록 하려고 한다. 이때 각 종류의 화폐는 몇개라도 사용 가능 
- 예를 들어 2,3 단위의 화폐가 있을 떄는 15원을 만들기 위해 3원을 5개사용하는 것이 가장 최소한의 화폐 개수이다. 
- M원을 만들기 위한 최소한의 화폐 개수를 출력하는 프로그램을 작성 

![image-20201117223704145](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201117223704145.png)ㅣ 

### 효율적인 화폐 구성 : 문제 해결 아이디어 

- a<sub>i</sub> = 금액 i를 만들 수 있는 최소한의 화폐 갯수 
- k = 각 화폐의 단위 
- 점화식 : 각 화폐 단위인 k를 __하나씩 확인하며__
  - a<sub>i-k</sub>를 만드는 방법이 존재하는 경우, a<sub>i</sub> = min(a<sub>i</sub> , a<sub>i-k</sub> +1)
  - a<sub>i-k</sub>를 만드는 방법이 존재하지 않는 경우, a<sub>i</sub> = INF  



- N=3, M= 7이고, 각 화폐의 단위가 2,3,5 인 경우 확인 

- Step 0 (초기화)

  - 먼저 각 인덱스에 해당하는 값으로 INF(무한) 값을 설정 
  - INF은 특정 금액을 만들 수 있는 화폐구성이 불가능하다는 의미 
  - 본 문제에서는 10001 

  ![image-20201117224119012](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201117224119012.png)

- Step 1

  - 첫번째 화폐 단위인 2를 확인 
  - 점화식에 따라 리스트가 갱신 

![image-20201117224354035](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201117224354035.png)

- Step 2 
  - 두번째 화폐 단위인 3를 확인 
  - 점화식에 따라서 다음과 같이 리스트가 갱신 

![image-20201117224450910](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201117224450910.png)

Step 3

- 세번째 화폐 단위인 5를 확인 
- 점화식에 따라서 다음과 같이 리스트가 최종적으로 갱신 

![image-20201117224531120](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201117224531120.png)

### 답안 예시 	

```python
n, m = map(int, input().split())

array = []
for i in range(n):
	array.append(int(input()))
    
d = [10001] * (m+1)
d[0] = 0

for i in range(n):
    for j in range(array[i], m+1):
        if d[j-array[i]] != 10001:
            d[j] = min(d[j], d[j- array[i]]+1)
if d[m] = 10001: 
    print(-1)
else: 
    print(d[m])
```



## 금광 : 문제 설명 

- n x m 크기의 금광이 있습니다. 금광은 1 x 1 크기의 칸으로 나누어져 있으며, 각 칸은 특정한 크기의 금이 들어 있습니다. 
- 채굴자는 첫 번째 열부터 출발하여 금을 캐기 시작합니다. 맨 처음에는 첫 번쨰 열의 어느 행에서든 출발할 수 있습니다. 이후에 m-1번에 걸쳐서 매번 오른쪽 위, 오른쪽, 오른쪽 아래 3가지 중 하나의 위치로 이동해야 합니다. 결과적으로 __채굴자가 얻을 수 있는 금의 최대 크기__를 출려하는 프로그램을 작성 

![image-20201117225141138](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201117225141138.png)

![image-20201117225211917](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201117225211917.png)

### 문제 해결 아이디어 

- 금광의 모든 위치에 대해 3가지만 고려 
  - 왼쪽 위에서 올때 / 왼쪽 아래서 올떄 / 왼쪽에서 올때 
- __세가지 경우__ 중에서 __가장 많은 금을 갖고 있는 경우__를 테이블에 갱신해주어 문제를 해결 
- array[ i ] [ j ] = i 행 j 열에 존재하는 금의 양 
- dp[ i ] [ j ] = i행 j열 까지의 최적의 해 (얻을 수 있는 금의 최댓값)

![image-20201117225425069](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201117225425069.png)

- 이때 테이블에 접근할 떄마다 리스트의 범위를 벗어나지 않는지 체크 
- 편의상 초기 데이터를 담는 변수 array 를 안써도 됨 
  - 바로 DP 테이블에 초기 데이터를 담아서 다이나믹 프로그래밍을 적용 가능 

![image-20201117225608415](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201117225608415.png)

```python
for tc in range(int(input())):
    n, m = map(int, input().split())
    array = list(map(int, input().split()))
    
    dp  = []
    index = 0
    
    for i in range(n):
        dp.append(array[index:index+m])
        index += m 
    for j in range(1,m):
        for i in range(n):
            if i==0: left_up = 0
            else: left_up = dp[i-1][j-1]
            
            if i== n-1: left_up = 0
            else: left_down = dp[i=1][j-1]
            left = dp[i][j-1]
            dp[i][j] = dp[i][j] +max(left_up, left_down, left)
    result = 0
    for i in range(n):
        result = max(result, dp[i][m-1])
    print(result)
```



## 병사 배치하기 : 문제 설명 

- N명의 병사가 무작위로 나열. 각 병사는 특정한 값의 전투력을 보유
- 병사를 배치할 떄는 __전투력이 높은 병사가 앞쪽에 오도록 내림차순으로 배치__ 
- 배치 과정에는 특정한 위치에 있는 병사를 열외시키는 방법 이용. 그러면서도 남아 있는 병사의 수가 최대로 하려고 한다.

![image-20201117230412810](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201117230412810.png)

![image-20201117230425656](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201117230425656.png)

## 문제 해결 아이디어 

- 이 문제의 기본 아이디어는 __가장 긴 증가하는 부분 수열(Longest Increasing Subsequence, LIS)__로 알려진 다이나믹 프로그래밍 문제
- ex) array = {4,2,5,8,4,11,15}
  - 이 수열의 가장 긴 증가하는 부분 수열은 {4,5,8,11,15}
- __본 문제는 가장 긴 감소하는 부분 수욜을 찾는 문제__로 치환할 수 있으므로, LIS 알고리즘을 조금 수정하여 적용 
- D[i] = array[i] 를 마지막 원소로 가지는 부분 수열의 최대 길이 
- 점화식 

![image-20201117230703962](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201117230703962.png)

![image-20201117230733771](C:\Users\scoji\AppData\Roaming\Typora\typora-user-images\image-20201117230733771.png)

- 가장 먼저 입력 받은 병사 정보의 순서를 뒤집 
- __가장 긴 증가하는 부분 수열(LIS)__ 알고리즘을 수행하여 정답을 도출 

```python
n = int(input())
array = list(map(int, input().split()))
array.reverse()

dp = [1] * n 

for i in range(1,n):
    for j in range(0,i):
        if array[j] < array[i]:
            dp[i] = max(dp[i], dp[j] +1)
print(n-max(dp))
```







