#选择排序

#概述
<img src = 'img/sort/select.gif'/>
可以看作是冒泡排序的改进版，省去了不断的元素交换，每次找出最大的元素
```
import java.util.Arrays;

public class selectSort {
	//核心思想 选出最小的，再交换

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		int[] arr = {2,6,4,3,0};
		selectSort(arr);
		System.out.println(Arrays.toString(arr));

	}

	public static void selectSort(int[] arr) {
		int min = 0;
		for(int i = 1; i <= arr.length - 1; i++) {
			min = i - 1;
			for(int j = i; j <= arr.length - 1; j++) {
				if(arr[j] < arr[min]) {
					min = j;
				}
			}
			swap(arr, i - 1, min);
		}
	}

	public static void swap(int[] arr, int i, int j) {
		int tmp = arr[i];
		arr[i] = arr[j];
		arr[j] = tmp;
	}

}
```
