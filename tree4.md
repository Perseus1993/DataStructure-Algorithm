#哈夫曼树

####讲解
构成哈夫曼树的步骤
1 从小到大排序，每个数据都是节点，每个节点都是简单二叉树
2 取出根节点权值最小的两个二叉树
3 组成一颗新的二叉树，新二叉树的根节点权值是前面两个二叉树节点权值的和
4 将新二叉树与其他二叉树重新排序，直到所有数据都被处理，就得到新的哈夫曼树

####代码
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

		//哈夫曼编码
		Map<Byte, String> huffmanCodes = getCodes(huffmanTreeRoot);

		System.out.println("哈夫曼表" + huffmanCodes);
	}

	//生成哈夫曼树对应的编码
	//思路
	//哈夫曼编码放到map中
	//在生成哈夫曼编码表需要拼接路径 用StringBuilder存储叶子结点的路径
	static StringBuilder sb = new StringBuilder();
	static Map<Byte, String> huffmanCodes = new HashMap<>();

	//叶子节点放入到集合中 node传入节点 code 路径（左1 右0）， sb拼接路径
	private static void getCodes(Node node, String code, StringBuilder sb) {
		StringBuilder sb2 = new StringBuilder(sb);
		sb2.append(code);
		if(node != null) {
			if(node.data == null) {
				//非叶子节点左右递归
				getCodes(node.left, "0", sb2);
				getCodes(node.right, "1", sb2);
			}else {
				huffmanCodes.put(node.data, sb2.toString());
			}
		}
	}
	//重载
	private static Map<Byte, String> getCodes(Node root){
		if(root != null) {
			return null;
		}
		getCodes(root.left, "0", sb);
		getCodes(root.right, "1", sb);
		return huffmanCodes;
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
