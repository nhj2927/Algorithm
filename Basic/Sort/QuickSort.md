# QuickSort

```java
import java.util.ArrayList;
import java.util.Arrays;

public class QuickSort {
	public ArrayList<Integer> sort(ArrayList<Integer> dataList) {
		if (dataList.size() <= 1) {
			return dataList;
		}
		int pivot = dataList.get(0);

		ArrayList<Integer> leftArr = new ArrayList<Integer>();
		ArrayList<Integer> rightArr = new ArrayList<Integer>();

		for(int i = 1; i < dataList.size(); i++) {
			if (pivot < dataList.get(i)) {
				rightArr.add(dataList.get(i));
			} else {
				leftArr.add(dataList.get(i));
			}
		}

		ArrayList<Integer> mergedArr = new ArrayList<Integer>();
		mergedArr.addAll(this.sort(leftArr));
		mergedArr.addAll(Arrays.asList(pivot));
		mergedArr.addAll(this.sort(rightArr));

		return mergedArr;
	}


}

```
