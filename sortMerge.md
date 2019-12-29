# 算法概述
归并排序体现了分治策略


# 代码
```java
package sort;

import java.util.Arrays;

public class sortMerge {

	public static void main(String[] args) {
		int[] arr = {3, 5, 4, 6, 2, 1, 7};
		int[] tmp = new int[arr.length];
		mergeSort(arr, 0, arr.length - 1, tmp);

		System.out.println(Arrays.toString(arr));

	}

	public static void mergeSort(int[] arr, int start, int end, int[] tmp) {
		if(start < end) {
			int mid = (start + end)/2;
			mergeSort(arr, start, mid, tmp);
			mergeSort(arr, mid + 1, end, tmp);
			merge(arr, start,mid, end, tmp);
		}


	}

	public static void merge(int[] arr, int leftStart,int mid, int rightEnd, int[] tmp) {
		if(leftStart < rightEnd) {
			int l = leftStart;
			int r = mid + 1;
			int tmpCount = leftStart;

			while(l <= mid && r <= rightEnd) {
				if(arr[l] <= arr[r]) {
					tmp[tmpCount] = arr[l];
					tmpCount++;
					l++;
				}else {
					tmp[tmpCount] = arr[r];
					tmpCount++;
					r++;
				}
			}
			while(l <= mid) {
				tmp[tmpCount] = arr[l];
				tmpCount++;
				l++;
			}
			while(r <= rightEnd) {
				tmp[tmpCount] = arr[r];
				tmpCount++;
				r++;
			}

			//拷贝到arr
			int tmpLeft = leftStart;
			while(tmpLeft <= rightEnd) {
				arr[tmpLeft] = tmp[tmpLeft];
				tmpLeft ++;
			}
		}else {

		}

	}

}

```
