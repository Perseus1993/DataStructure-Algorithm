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
