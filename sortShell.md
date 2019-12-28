#算法概述
希尔排序

```java
public static void method(int[] arr) {
		int tmp;
		for(int gap = arr.length/2; gap > 0; gap /= 2 ) {
			for(int i = gap; i < arr.length; i++) {
				for(int j = i; j - gap>= 0; j -= gap) {
					if(arr[j] < arr[j - gap]) {
						tmp = arr[j];
						arr[j] = arr[j - gap];
						arr[j - gap] = tmp;
					}
				}
			}
		}
	}
```
