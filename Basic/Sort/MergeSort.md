# MergeSort

```java
import java.util.ArrayList;

public class MergeSort {
	public ArrayList<Integer> mergeSplitFunc(ArrayList<Integer> dataList) {
		if (dataList.size() <= 1) {
			return dataList;
		}
		int medium = dataList.size() / 2;

		ArrayList<Integer> leftArr = mergeSplitFunc(new ArrayList<Integer>(dataList.subList(0, medium)));
		ArrayList<Integer> rightArr = mergeSplitFunc(new ArrayList<Integer>(dataList.subList(medium, dataList.size())));

		return mergeFunc(leftArr, rightArr);
	}

	public ArrayList<Integer> mergeFunc(ArrayList<Integer> leftArr, ArrayList<Integer> rightArr) {
		int i = 0, j = 0;
		ArrayList<Integer> mergedArr = new ArrayList<Integer>();

		while(i < leftArr.size() && j < rightArr.size()) {
			if (leftArr.get(i) < rightArr.get(j)) {
				mergedArr.add(leftArr.get(i));
				i++;
			} else {
				mergedArr.add(rightArr.get(j));
				j++;
			}
		}

        // rightArr에 데이터가 남았을때
		if (i >= leftArr.size()) {
			for (int k = j; k < rightArr.size(); k++) {
				mergedArr.add(rightArr.get(k));
			}
		} else {
			for (int k = i; k < leftArr.size(); k++) {
				mergedArr.add(leftArr.get(k));
			}
		}

		return mergedArr;
	}
}
```
