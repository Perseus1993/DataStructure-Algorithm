#顺序化二叉树

```java
package tree2;

public class ArrBinaryTreeDemo {

	public static void main(String[] args) {
		int[] arr = {1, 2, 3, 4, 5, 6, 7};
		ArrayBinaryTree  ab = new ArrayBinaryTree(arr);

	}

}

class ArrayBinaryTree{
	private int[] arr;

	public ArrayBinaryTree(int[] arr) {
		this.arr = arr;
	}
	public void preOrder() {
		this.preOrder(0);
	}
	public void preOrder(int index) {
		if(arr == null || arr.length ==0) {
			System.out.println("数组为空");
		}
		System.out.println(arr[index]);

		if((index * 2 + 1) < arr.length) {
			preOrder(2 * index + 1);
		}

		if((index * 2 + 2) < arr.length) {
			preOrder(2 * index + 2);
		}
	}
	public void midSearch(int index) {
		if(arr == null || arr.length ==0) {
			System.out.println("数组为空");
		}
		if((index * 2 + 1 < arr.length)) {
			midSearch(index * 2 + 1);
		}

		System.out.println(arr[index]);

		if((index * 2 + 1 < arr.length)) {
			midSearch(index * 2 + 2);
		}
	}

	public void postSearch(int index) {
		if(arr == null || arr.length ==0) {
			System.out.println("数组为空");
		}
		if((index * 2 + 1 < arr.length)) {
			midSearch(index * 2 + 1);
		}
		if((index * 2 + 1 < arr.length)) {
			midSearch(index * 2 + 2);
		}

		System.out.println(arr[index]);


	}
}

```
