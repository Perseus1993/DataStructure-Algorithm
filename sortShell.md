#算法概述
插入排序对于大规模的乱序数组速度比较慢，因为要不停地比较。如果当前待插入元素是数组中最小的，插入到合适位置就需要比较整个数组，为了加快这一过程，希尔排序交换不相邻元素对数组局部进行排序。

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
