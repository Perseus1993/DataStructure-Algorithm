#哈夫曼树

####讲解
构成哈夫曼树的步骤
1 从小到大排序，每个数据都是节点，每个节点都是简单二叉树
2 取出根节点权值最小的两个二叉树
3 组成一颗新的二叉树，新二叉树的根节点权值是前面两个二叉树节点权值的和
4 将新二叉树与其他二叉树重新排序，直到所有数据都被处理，就得到新的哈夫曼树

####代码
```java
public class HuffmanTree {

	public static void main(String[] args) {
		int[] arr = { 13, 7, 8, 3, 29, 6, 1 };
		Node root = createHuffmanTree(arr);
		preOrder(root);

	}

	public static void preOrder(Node root) {
		if(root != null) {
			root.preOrder();
		}else {
			System.out.println("空树");
		}
	}

	public static Node createHuffmanTree(int[] arr) {
		// 1.遍历数组
		// 2.arr构成node
		// 3.Node放入arrayList
		List<Node> nodes = new ArrayList<Node>();
		for (int value : arr) {
			nodes.add(new Node(value));
		}

		while (nodes.size() > 1) {
			Collections.sort(nodes);
			System.out.println(nodes);

			// 取出根节点最小的二叉树
			Node leftNode = nodes.get(0);
			Node rightNode = nodes.get(1);
			Node parent = new Node(leftNode.value + rightNode.value);
			parent.left = leftNode;
			parent.right = rightNode;
			// 删除掉处理过的二叉树
			nodes.remove(leftNode);
			nodes.remove(rightNode);

			nodes.add(parent);

		}
		return nodes.get(0);
	}

}

//为了让node支持排序，需要实现comparable接口
class Node implements Comparable<Node> {
	int value;// 节点权值
	Node left;
	Node right;

	public Node(int value) {
		this.value = value;
	}

	@Override
	public String toString() {
		return "Node [value=" + value + "]";
	}

	@Override
	public int compareTo(Node o) {
		// 从小到大排序
		return this.value - o.value;
	}
	//前序遍历
	public void preOrder() {
		System.out.println(this);
		if(this.left != null) {
			this.left.preOrder();
		}
		if(this.right != null) {
			this.right.preOrder();
		}
	}


}

```

#### 哈夫曼编码
功能：把字符串对应的哈夫曼树

思路
1. Node{data(存放数据)， weight(权值)， left, right}
2. 对应的byte[]
3. 将节点放到list中
4. 通过list创建哈夫曼树

```java
public class HuffmanCode {

	public static void main(String[] args) {
		String content = "i like like like java do you like a java";
		byte[] contentBytes = content.getBytes();
		System.out.println(contentBytes.length);
		List<Node> nodes = getNodes(contentBytes);
		System.out.println(nodes);

		System.out.println("树");
		Node huffmanTreeRoot = createHuffmanTree(nodes);
		System.out.println("前序遍历");
		huffmanTreeRoot.preOrder();
	}

	public static void preOrder(Node root) {
		if(root != null) {
			root.preOrder();
		}else {
			System.out.println("空的啊");
		}
	}

	private static List<Node> getNodes(byte[] bytes){
		//创建arraylist
		ArrayList<Node> nodes = new ArrayList<Node>();
		//统计出现次数
		Map<Byte, Integer> counts = new HashMap<>();
		for(byte b : bytes) {
			Integer count = counts.get(b);
			if(count == null) {
				counts.put(b, 1);
			}else {
				counts.put(b, count + 1);
			}
		}
		//每个键值对转成node
		for(Map.Entry<Byte, Integer> entry : counts.entrySet()) {
			nodes.add(new Node(entry.getKey(), entry.getValue()));
		}
		return nodes;
	}
	//创建树
	private static Node createHuffmanTree(List<Node> nodes) {
		while(nodes.size() > 1) {
			Collections.sort(nodes);
			Node leftNode = nodes.get(0);
			Node rightNode = nodes.get(1);
			Node parent = new Node(null, leftNode.weight + rightNode.weight);
			parent.left = leftNode;
			parent.right = rightNode;

			nodes.remove(leftNode);
			nodes.remove(rightNode);
			nodes.add(parent);
		}
		return nodes.get(0);
	}

}

class Node implements Comparable<Node>{
	Byte data;
	int weight;
	Node left;
	Node right;
	public Node(Byte data, int weight) {
		super();
		this.data = data;
		this.weight = weight;
	}
	@Override
	public int compareTo(Node o) {
		// TODO Auto-generated method stub
		return this.weight - o.weight;
	}
	@Override
	public String toString() {
		return "Node [data=" + data + ", weight=" + weight + "]";
	}
	public void preOrder() {
		System.out.println(this);
		if(this.left != null) {
			this.left.preOrder();;
		}
		if(this.right != null) {
			this.right.preOrder();;
		}
	}
}
```
