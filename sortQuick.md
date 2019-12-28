#快速排序
快排在面试中经常被考到，主要难点在于边界条件的确定以及递归的使用。在这里使用的是用第一个元素作为pivot（轴）的方法

快排的核心思想就是选取一个元素作为轴，使轴左边的元素小于轴，右边的元素大于轴，再把快排递归调用再轴的两侧

循序渐进，
第一步考虑如何实现归位轴左右的元素：
第二部考虑边界条件
第三步考虑递归的使用

第一步的思路就是把第一个元素作为轴pivot，从下一个元素到末尾的范围中（设为i，j），i逐渐增长直到遇到比pivot大的数字，j逐渐减小直到遇到比pivot小的数字，交换i，j索引的元素，再进一步增长，直到i j碰头

第二部思考边界条件

i,j不断交换到最后，pivot是和j做交换，所以要保住j不要越界，j是从末尾向前冲，最极端的情况是所有的元素都大于j，因此j冲到了索引是1的位置

```java
public class QuickSort {

	public static void main(String[] args) {
		int[] arr = {9, 8, 6, 5, 5, 5,2,9};
		method(arr,0,arr.length - 1);
		System.out.println(Arrays.toString(arr));

	}
	public static void  method(int[] arr, int start, int end) {
		if(start < end) {
			int pivot = arr[start];
			int i = start + 1;
			int j = end;
			while(i < j) {
				while(i <= j && arr[i] <= pivot) {
					i++;
				}
				while(i <= j && arr[j] > pivot) {
					j--;
				}
				if(i <= j) {
					swap(arr, i, j);
				}
			}
			swap(arr, start, j);
			method(arr,j + 1, end);
			method(arr,start, j - 1);
		}

	}
	public static void swap(int[] arr, int i, int j) {
		int tmp = arr[i];
		arr[i] = arr[j];
		arr[j] = tmp;
	}

}

```
