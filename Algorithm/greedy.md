## 그리디 알고리즘
* 그리디 알고리즘(탐욕법)은 현재 상황에서 지금 당장 좋은 것만 고르는 방법의 의미한다.
* 일반적인 그리디 알고리즘은 문제를 풀기 위한 최소한의 아이디어를 떠올릴 수 있는 능력을 요구한다
* 그리디 해법은 그 정당성 분석이 중요하다.
* 단순히 가장 좋아 보이는 것을 반복적으로 선택해도 최적의 해를 구할 수 있는지 검토한다.

* 일반적인 상황에서 그리디 알고리즘은 최적의 해를 보장할 수 없을 때가 많다
* 하지만 코딩 테스트에서의 그리디 문제는 대부분 탐욕법으로 얻은 해가 최적의 해가 되는 상황에서, 이를 추론할 수 있어야 풀리도록 출제됩니다.

### 예제 문제 : 거스름돈
* 당신은 음식점의 계산을 도와주는 점원입니다. 카운터에는 거스름돈으로 사용할 500원, 100원, 50원, 10원이 무한히 존재한다고 가정한다. 손님에게 거슬러 주어야 할 돈이 N원일 때 거슬러 주어야할 동전의 최소 개수를 구하라. 거슬러줘야 할 돈 N은 항상 10의 배수이다.

* 문제 해결 아이디어
    + 최적의 해를 빠르게 구하기 위해서는 가장 큰 화폐 단위부터 돈을 거슬러 주면 된다.
    + N원을 거슬러 줘야 할 때, 가장 먼저 500원으로 거슬러 줄 수 있을 만큼 거슬러 준다.
       - 이후에 100원, 50원, 10원짜리 동전을 차례대로 거슬러 줄 수 있을만큼 거슬러 주면 된다.
    
* 정당성 분석
    + 가장 큰 화폐 단위부터 돈을 거슬러 주는 것이 최적의 해를 보장하는 이유는 무엇인가?
        - 가지고 있는 동전 중에서 큰 단위가 항상 작은 단위의 배수이므로, 작은 단위의 동전들을 종합해 다른 해가 나올 수 없기 때문이다.
    + 만약에 800원을 거슬러 주어야 하는데, 화폐 단위가 500원 400원 100원이라면 어떻게 되는가?
    + 그리디 알고리즘에서는 이처럼 문제 풀이를 위한 최소한의 아이디어를 떠올리고 이것이 정당한지 검토할 수 있어야 한다.

* 답안 예시
```python
N = 1260 # N이 1260이라는 예시
cnt = 0

# 큰 단위의 화폐부터 차례대로 확인하기
array = [500, 100, 50, 10]
for coin in array:
    count += n // coin # 해당 화폐로 거슬러 줄 수 있는 동전의 개수 세기
    n %= coin

print(count)
```

* 시간복잡도 분석
    + 화폐의 종류가 K라고 할 때, 소스코드의 시간 복잡도는 O(k)이다.
    + 이 알고리즘의 시간 복잡도는 거슬러줘야 하는 금액과는 무관하며, 동전의 총 종류에만 영향을 준다.


### 예제 문제 2 : 1이 될 때 까지
* 어떠한 수 N이 1이 될 때까지 다음의 두 과정 중 하나를 반복적으로 선택하여 수행하려고 한다. 단, 두 번째 연산은 N이 K로 나누어 떨어질 때만 선택할 수 있다.
    1. N에서 1을 뺀다.
    2. N을 K로 나눈다.
* 예를 들어 N이 17, K가 4 라고 가정하자. 이 때 1번의 과정을 한 번 수행하면 N은 16이 된다. 이후에 2번의 과정을 두 번 수행하면 N은 1이 됩니다. 결과적으로 이 경우 전체 과정을 실행한 횟수는 3이 된다. 이는 N을 1로 만드는 최소 횟수이다.
* N과 K가 주어질 때 N이 1이 될 때 까지 1본 혹은 2번의 과정을 수행해야 하는 최소 횟수를 구하는 프로그램을 작성해보시오.

* 문제 해결 아이디어
    + 주어진 N에 대하여 최대한 많이 나누기를 수행하면 된다.
    + N의 값을 줄일 때 2 이상의 수로 나누는 작업이 1을 빼는 작업보다 수를 훨씬 많이 줄일 수 있다.

* 정당성 분석
    + 가능하면 최대한 많이 나누는 작업이 최적의 해를 항상 보장할 수 있는가?
    + N이 아무리 큰 수여도,  K로 계속 나눈다면 기하급수적으로 빠르게 줄일 수 있다.
    + 다시 말해 K가 2 이상이기만 한다면, K로 나누는 것이 1을 빼는 것보다 항상 빠르게 N을 줄일 수 있다.
        - 또한 N은 항상 1에 도달하게 된다(최적의 해 성립).

* 답안 예시
```python
n, k = map(int, input().split())

result = 0

while True:
    # n이 k로 나누어 떨어지는 수가 될 때까지 빼기
    target = (n // k) * k # 이렇게 한 이유 : n이 k로 나누어 떨어지지 않는다고 했을 때 가장 가까운 k로 나누어 떨어지는 수가 어떤건지 사용할 수 있음
    result += (n - target) # 1을 빼는 연산을 한 횟수
    n = target
    # n이 k보다 작을 때(더 이상 나눌 수 없을 때) 반복문 탈출
    if n < k:
        break
    result += 1
    n //= k

# 마지막으로 남은 수에 대하여 1씩 빼기
result += (n - 1)
print(result)
```

### 예제 문제 3 : 곱하기 혹은 더하기
*  문제 설명
    + 각 자리가 숫자(0부터 9)로만 이루어진 문자열 S가 주어졌을 때, 왼쪽부터 오른쪽으로 하나씩 모든 숫자를 확인하며 숫자 사이에 'x' 혹은 '+' 연산자를 넣어 결과적으로 만들어질 수 있는 가장 큰 수를 구하는 프로그램을 작성하라. 단 +보다 x를 먼저 계산하는 일반적인 방식과 달리, 모든 연산은 왼쪽에서부터 순서대로 이루어진다고 가정한다.
    + 예를 들어 02984라는 문자열로 만들 수 있는 가장 큰 수는 ((((0 + 2) * 9) * 8) * 4) = 576이다. 또한 만들어질 수 있는 가장 큰 수는 항상 20억 이하의 정수가 되도록 입력이 주어진다.

* 문제 해결 아이디어
    + 대부분의 경우 + 보다는 *가 값을 더 크게 만든다.
        - 예를 들어 5+6 11이고 5*6은 30이다.
    + 다만 두 수중에서 하나라도 '0' 혹은 '1'인 경우, 곱하기보다는 더하기를 수행하는 것이 효율적이다.
    + 따라서 두 수에 대하여 연산을 수행할 때, 두 수 중에서 하나라도 1 이하인 경우에는 더하며, 두 수가 모두 2 이상인 경우에는 곱하면 된다. 

* 답안 예시
```python
data = input()

# 첫 번째 문자를 숫자로 변경하여 대입
result = int(data[0])

for i in range(1, len(data)):
    # 두 수 중에서 하나라도 '0' 혹은 '1'인 경우, 곱하기 보다는 더하기 수행
    num = int(data[i])
    if num <= or result <= 1:
        result += num
    else:
        result =*= num

print(result)
```