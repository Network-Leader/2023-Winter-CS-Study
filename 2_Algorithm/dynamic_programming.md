# Dynamic Programming

### 개념

- 하나의 큰 문제를 여러 개의 작은 문제로 나누어 그 결과를 저장한 뒤, 다시 그 큰 문제를 해결하는 방법 -> memoization
- 이미 했던 연산을 반복하는 경우를 보완

* 시간복잡도
  배열의 크기(혹은 테이블의 크기) X 한 칸을 채울때 걸리는 시간
  최악의 경우 n번째 항까지 배열을 채워야 하기 때문에 배열의 크기는 n, 한칸을 채우는 데에 걸리는 시간은 일정한 시간, 즉 1
  ->O(n)<br/>  
  <br/>

### 조건

#### 최적 부분 구조

작은 문제들의 최적의 답을 이용하여 큰 문제의 최적의 답을 구할 수 있음
큰 문제의 답에 작은 문제의 답이 포함되어 있음
큰 문제와 작은 문제의 관계에서 사이클이 존재해서는 안 됨

#### 부분 문제 반복

작은 문제의 답을 재활용할 수 있어야 하기 때문에 동일한 부분 문제가 반복적으로 등장
한 번 구했던 답이 나중에도 사용<br/>  
<br/>

### 풀이 종류

#### Botton-Up

- 작은 문제부터 해결
- for문 이용
- 재귀 호출이 없어 시간과 메모리 절약 가능
- 직관적으로 이해하기 힘들 수도 있음

```
int save[100];
int DP(int x)
{
    save[0] = 0; save[1] = 1;
    for(int i = 2; i <= n; i++)
        save[i] = save[i - 1] + save[i - 2];
    return save[x];
}
```

#### Top-Down

- 큰 문제부터 해결
- 재귀 이용
- 전에 계산해 둔 값이 있으면 쓰고 없으면 계산
- 최대 재귀 깊이 초과 에러 발생 가능성
- 이해하기 쉬운 점화식
- 서브 문제 전체의 크기에 비해 메인 문제에 관여하는 적은 경우 사용

```
int save[100];
int DP(int x)
{
    if (x == 1) return 1;
    if (x == 2) return 1;
    if (save[x] != 0) return save[x];
    return save[x] = DP(x - 1) + DP(x + 1);
}
```

<br/>  
<br/>

#### 피보나치 수열을 이용한 예시

recursion

```
int fibo_recur(int n) {
	if(n==0) return 0;
	else if (n == 1) return 1;
	return fibo_recur(n - 1) + fibo_recur(n - 2);
}
```

DP (Top-Down)

```
double fibo_DP(int n) {
	int fibo_memo[100];
	fibo_memo[0] = 0;
	fibo_memo[1] = 1;

	if (fibo_memo[n] > 0) return fibo_memo[n];
	if ((n == 0) || (n == 1)) return fibo_memo[n];
	return fibo_memo[n] = fibo_DP(n - 1) + fibo_DP(n - 2);
}
```

반복문 (Bottom-Up)

```
double fibo_for(int n) {
	int fibo_memo[100];
	fibo_memo[0] = 0;
	fibo_memo[1] = 1;

	if (n == 0) return fibo_memo[n];
	else if (n == 1) return fibo_memo[n];

	for (int i = 2; i < n; i++)
			fibo_memo[i] = fibo_memo[i - 1] + fibo_memo[i - 2];

	return fibo_memo[n - 1] + fibo_memo[n - 2];
}
```

## 참고자료

https://ansohxxn.github.io/algorithm/dp/  
https://velog.io/@dlgosla/%EA%B0%9C%EB%85%90-%EC%A0%95%EB%A6%AC-%EB%8F%99%EC%A0%81-%EA%B3%84%ED%9A%8D%EB%B2%95DP-Dynamic-Programming
