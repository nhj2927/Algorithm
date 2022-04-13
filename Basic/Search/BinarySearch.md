# BinarySearch

```java
import java.util.ArrayList;

public class BinarySearch {
	public boolean searchFunc(ArrayList<Integer> dataList, Integer searchItem) {
		if (dataList.size() == 1 && dataList.get(0) == searchItem) {
			return true;
		}
		if (dataList.size() == 1 && dataList.get(0) != searchItem) {
			return false;
		}
		if (dataList.size() == 0) {
			return false;
		}

		int medium = dataList.size() / 2;
		if (dataList.get(medium) == searchItem) {
			return true;
		} else {
			if (dataList.get(medium) > searchItem) {
				return searchFunc(new ArrayList<Integer>(dataList.subList(0, medium)), searchItem);
			} else {
				return searchFunc(new ArrayList<Integer>(dataList.subList(medium, dataList.size())), searchItem);
			}
		}
	}
}

```
