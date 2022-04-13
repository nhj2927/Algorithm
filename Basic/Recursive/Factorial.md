# Factorial

- 정수 4를 1, 2, 3의 조합으로 나타내는 방법은 다음과 같이 총 7가지가 있음
- 정수 n이 입력으로 주어졌을 때, n을 1, 2, 3의 합으로 나타낼 수 있는 방법의 수를 구하시오
<pre>
1+1+1+1
1+1+2
1+2+1
2+1+1
2+2
1+3
3+1
</pre>

힌트: 정수 n을 만들 수 있는 경우의 수를 리턴하는 함수를 f(n) 이라고 하면,<br>
f(n)은 f(n-1) + f(n-2) + f(n-3) 과 동일하다는 패턴 찾기<br>
출처: ACM-ICPC > Regionals > Asia > Korea > Asia Regional - Taejon 2001

<br>

```java
public class Factorial {
	public int factorialFunc(int n) {
		if (n == 1) {
			return 1;
		}
		else if (n == 2) {
			return 2;
		}
		else if (n == 3) {
			return 4;
		}
		else {
			return factorialFunc(n - 1) + factorialFunc(n - 2) + factorialFunc(n - 3);
		}
	}
}

```
