
####包含内容
<ul background-color: grey>
<li>算法概述</li>
<li>普通版冒泡排序</li>
<li>改进版冒泡排序</li>
</ul>


##1.算法概述
<img src = 'img/sort/bubble.gif'/>


冒泡排序是一种经典排序算法，在数组中两两比对相邻元素，大的换到小的右边。每次都把最大的数换到最右端，确定当前最大数之后下一趟两两比较就不带这个数玩了。
总之记住核心思想就能写出代码：双层循环，外层代表每次确定末尾的最大数，内层代表从前到后两两比较的的过程。

边界条件记好：<br>
①外层循环(确定末尾最大)总共要arr.length - 1次<br>
②内层循环从索引0比相邻右边的元素 —> 索引（arr.length - 2 - '确定末尾最大'的次数）比相邻右边的元素

双层循环，复杂度n^2

##2.普通版冒泡排序

```java
//案例数组
int[] arr = {3, 9, -1, 10, -2};

public class Bubble {

	public static void bubbleSort(int[] arr) {
		for(int i = 0; i <= arr.length - 1; i++) {
			for(int j = 0; j <= arr.length - 2 - i; j++) {
				if(arr[j] > arr[j + 1]) {
					swap(arr, j, j + 1);
				}
			}
		}
		System.out.println(Arrays.toString(arr));
	}
  //交换数组中两个元素
	public static void swap(int[] arr, int i, int j) {
		int tmp = arr[i];
		arr[i] = arr[j];
		arr[j] = tmp;
	}
}

```
##3.改进版冒泡排序
在这里加入一个判断：当某一趟把最大的数向右边赶的时候，如果发现整个过程并没有发生元素交换，说明数组已经有序，提前退出循环<br>
时间复杂度不变
```java
public class Bubble {

	public static void bubbleSort(int[] arr) {
		boolean flag;

		for(int i = 0; i <= arr.length - 1; i++) {
			flag = false;
			for(int j = 0; j <= arr.length - 2 - i; j++) {
				if(arr[j] > arr[j + 1]) {
					flag = true;
					swap(arr, j, j + 1);
				}
			}
			if(!flag) {
				break;
			}
		}
		System.out.println(Arrays.toString(arr));
	}
```
