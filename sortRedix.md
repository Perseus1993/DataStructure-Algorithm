#基数排序
<img src = 'img/sort/sortMerge.gif'/>

#注意事项

#代码

```java
public class sortRadix {

	public static void main(String[] args) {
		int[] arr = {53, 3, 542, 748, 14, 214};
		method(arr);
		System.out.println(Arrays.toString(arr));

	}

	public static void method(int[] arr) {
		//找出最大
		int max = arr[0];
		for(int i = 0; i < arr.length; i++) {
			if(arr[i] > max) {
				max = arr[i];
			}
		}

		int maxLength = (max + "").length();


		//建桶
		int[][] bucket = new int[9][arr.length];
		//桶内元素个数索引
		int[] numBucket= new int[9];
		for(int i = 0, n = 1; i < maxLength; i++, n *= 10 ) {
			for(int j = 0; j < arr.length; j++) {
				int whichBucket = arr[j] / n % 10;
				bucket[whichBucket][numBucket[whichBucket]] = arr[j];
				numBucket[whichBucket]++;

			}
			//按顺序复制回去
			int count = 0;
			for(int k = 0; k < bucket.length; k++) {
				if(numBucket[k] != 0) {
					for(int l = 0; l < numBucket[k]; l++) {
						arr[count++] = bucket[k][l];
					}
				}
				numBucket[k] = 0;
			}
		}
	}

}
```
