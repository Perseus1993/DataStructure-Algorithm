####包含内容
<ul background-color: grey>
<li>算法概述</li>
<li>算法实现1</li>
<li>算法实现12</li>
</ul>

#概述
<img src = 'img/sort/insert.gif'/>

插入排序就像是扑克牌的抓取与排序，不断将未排序数组的第一个插到已经排序的有序数组中。核心思想就是两层循环，外层从第二个元素遍历到最后一个，内层是当前遍历元素向前寻找比较（挨个比较，遇到比自己小的就停下来，遇到比自己大的，就让大的元素向后移动）。

边界条件
外层索引1增大到arr.length - 1, 内层是（外层索引 - 1）减小到索引0，内层有两个终止条件：哨兵元素比索引0还小  or 当前元素 <= 哨兵元素
双层循环，妥妥n^2复杂度

#算法实现1
```
import java.util.Arrays;

public class InsertSort {

	public static void main(String[] args) {
    //示例数组
		int[] arr = { 100, 30, 46, 3 };
		method(arr);
		System.out.println(Arrays.toString(arr));

	}

	public static void method(int[] arr) {

		int tmp;
		for(int i = 1; i < arr.length; i++) {
			tmp = arr[i];
			for(int j = i - 1; j >= 0; j-- ) {
				//小坑：要用tmp判断！
				if(arr[j] <= tmp) {
					arr[j + 1] = tmp;
					break;
				}
				else {
					arr[j + 1] = arr[j];
					if(j == 0) {
						arr[j] = tmp;
					}
				}			
			}
		}
	}

}

```
#算法实现2
```
public class InsertSort2 {

	public static void main(String[] args) {
		int[] arr = {4, 5, 1, 10, 2};
		method(arr);

	}
	public static void method(int[] arr) {
		for(int i = 1; i < arr.length; i++) {
			int tmp = arr[i];
			int j = i - 1;
			//注意这里有个小坑while语句里面的判断顺序不能颠倒哦
			while( j >= 0 && tmp < arr[j]) {
				arr[j + 1] = arr[j];
				j--;

			}
			arr[j + 1] = tmp;
		}
		System.out.println(Arrays.toString(arr));
	}

}
```
