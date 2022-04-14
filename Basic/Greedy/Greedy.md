# Greedy

### 문제1: 동전 문제

- 지불해야 하는 값이 4720원 일 때 1원 50원 100원, 500원 동전으로 동전의 수가 가장 적게 지불하시오.
  - 가장 큰 동전부터 최대한 지불해야 하는 값을 채우는 방식으로 구현 가능
  - 탐욕 알고리즘으로 매순간 최적이라고 생각되는 경우를 선택하면 됨

<br>

### 문제2: 부분 배낭 문제 (Fractional Knapsack Problem)

- 무게 제한이 k인 배낭에 최대 가치를 가지도록 물건을 넣는 문제
  - 각 물건은 무게(w)와 가치(v)로 표현될 수 있음
  - 물건은 쪼갤 수 있으므로 물건의 일부분이 배낭에 넣어질 수 있음, 그래서 Fractional Knapsack Problem 으로 부름
    - Fractional Knapsack Problem 의 반대로 물건을 쪼개서 넣을 수 없는 배낭 문제도 존재함 (0/1 Knapsack Problem 으로 부름)
      <img src="https://www.fun-coding.org/00_Images/knapsack.png">

<br>

```java
import java.util.ArrayList;
import java.util.Arrays;

public class GreedyAlgorithm {
	public void coinFunc(Integer price, ArrayList<Integer> coinList) {
		int totalCoinCount = 0;
		int coinNum = 0;

		for (int i = 0; i < coinList.size(); i++) {
			coinNum = price / coinList.get(i);
			totalCoinCount += coinNum;
			price = price % coinList.get(i);
			System.out.println(coinList.get(i) + "원: " + coinNum + "개");
		}

		System.out.println("총 동전 갯수: " + totalCoinCount);
	}

	public void knapsackFunc(Integer[][] objectList, double capacity) {
		double totalValue = 0;
		double fraction;

		Arrays.sort(objectList, (arr1, arr2) -> {
			double value1 = arr1[1].doubleValue() / arr1[0];
			double value2 = arr2[1].doubleValue() / arr2[0];

			if (value1 > value2) {
				return -1;
			} else if (value1 == value2) {
				return 0;
			} else {
				return 1;
			}
		});

		for(int i = 0; i < objectList.length; i++) {
			if (capacity <= 0) {
				break;
			}

			if ((capacity - objectList[i][0]) >= 0) {
				capacity -= objectList[i][0];
				totalValue += objectList[i][1];
				System.out.println("무게:" + objectList[i][0] + ", 가치:" + objectList[i][1]);
			} else {
				fraction = capacity / objectList[i][0];
				totalValue += fraction * objectList[i][1];
				System.out.println("무게:" + objectList[i][0] + ", 가치:" + objectList[i][1] + ", 비율:" + fraction);
				break;
			}
		}

		System.out.println("총 담을 수 있는 가치:" + totalValue);
	}
}

```
