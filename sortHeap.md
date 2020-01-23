#堆排序

####基本思想
1将无序序列构建成一个堆，根据升序降序选择大顶堆或小顶堆
2将堆顶元素与末尾元素交换，将最大元素沉到数组末端
3重新调整结构，使其满足堆定义，然后继续交换堆顶元素和当前末尾元素，反复执行+交换步骤，直到整个序列有序
####代码
```java
package sort;

public class HeapSort {

	public static void main(String[] args) {
		int[] arr = {4, 6, 8, 5, 9};

	}
	public void heapSort(int[] arr){
		int temp = 0;
		for(int i = arr.length / 2 - 1 ; i >= 0; i--) {
		}
		for(int j = arr.length - 1; j > 0; j--) {
			temp = arr[j];
			arr[j] = arr[0];
			arr[0] = temp;
			adjust(arr, 0, j);
		}
	}
	//将数组调整成大顶堆
	//i 是非叶子节点在数组中的索引，length表示多少元素调整（逐渐减少）
	public static void adjust(int[] arr, int i, int length) {
		int tmp = arr[i];//取出当前元素
		for(int k = i * 2 + 1; k < length; k = k* 2 + 1) {
			if(k < length && arr[k] < arr[k + 1]) {
				//左子节点大于右子节点		
				k++;
			}
			//子节点大于父节点
			if(arr[k] > tmp){
				arr[i] = arr[k];
				i = k;
			}else {
				break;
			}
		}
		//for循环结束后，以i为父节点的树的最大值，放在了最顶
		arr[i] = tmp;
	}

}

```
