#Selection Sort

```java
import java.util.ArrayList;
import java.util.Collections;

public class SelectionSort {
	public ArrayList<Integer> sort(ArrayList<Integer> dataList) {
		for (int i = 0; i < dataList.size() - 1; i++) {
			int min = i;
			for (int j = i + 1; j < dataList.size(); j++) {
				if (dataList.get(min) > dataList.get(j)) {
					min = j;
				}
			}
			Collections.swap(dataList, i, min);
		}
		return dataList;
	}
}

```
