#简单二叉树

具有谦虚，中序，后续遍历查找功能

```java
public class BinaryTreeDemo {

	public static void main(String[] args) {
		binaryTree tree = new binaryTree();
		HeroNode root = new HeroNode(1, "松江");
		HeroNode node2 = new HeroNode(2, "武松");
		HeroNode node3 = new HeroNode(3, "乃功");
		HeroNode node4 = new HeroNode(4, "川地");
		HeroNode node5 = new HeroNode(5, "巨无霸");

		//先手动创建
		root.setLeft(node2);
		root.setRight(node3);
		node3.setRight(node4);
		node3.setLeft(node5);

		tree.setRoot(root);
//		tree.preOrder();
		System.out.println(tree.postOrderSearch(2));


	}

}
class binaryTree{
	private HeroNode root;

	public void setRoot(HeroNode root) {
		this.root = root;
	}
	public void preOrder() {
		if (root != null) {
			this.root.preOrder();
		}else {
			System.out.println("树空");
		}
	}
	public void mideOrder() {
		if (root != null) {
			this.root.midOrder();
		}else {
			System.out.println("树空");
		}
	}
	public void postOrder() {
		if (root != null) {
			this.root.postOrder();
		}else {
			System.out.println("树空");
		}
	}

	public HeroNode preOrderSearch(int no) {
		if(root != null) {
			return root.preOrderSearch(no);
		}else {
			System.out.println("树空");
			return null;
		}
	}
	public HeroNode midOrderSearch(int no) {
		if(root != null) {
			return root.midOrderSearch(no);
		}else {
			System.out.println("树空");
			return null;
		}
	}
	public HeroNode postOrderSearch(int no) {
		if(root != null) {
			return root.postOrderSearch(no);
		}else {
			System.out.println("树空");
			return null;
		}
	}




}

//创建节点
class HeroNode{
	private int id;
	private String name;
	private HeroNode left;
	private HeroNode right;
	public int getId() {
		return id;
	}
	public void setId(int id) {
		this.id = id;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public HeroNode getLeft() {
		return left;
	}
	public void setLeft(HeroNode left) {
		this.left = left;
	}
	public HeroNode getRight() {
		return right;
	}
	public void setRight(HeroNode right) {
		this.right = right;
	}
	public HeroNode(int id, String name) {
		super();
		this.id = id;
		this.name = name;
	}
	@Override
	public String toString() {
		return "HeroNode [id=" + id + ", name=" + name + "]";
	}

	//前序遍历
	public void preOrder() {
		System.out.println(this);
		//递归左子树
		if(this.left != null) {
			this.left.preOrder();
		}

		if(this.right != null) {
			this.right.preOrder();
		}
	}

	//中序遍历
	public void midOrder() {
		if(this.left != null) {
			this.left.midOrder();
		}
		System.out.println(this);

		if(this.right != null) {
			this.right.midOrder();
		}
	}

	public void postOrder() {
		if(this.right != null) {
			this.right.midOrder();
		}
		System.out.println(this);
		if(this.left != null) {
			this.left.midOrder();
		}				

	}

	public HeroNode preOrderSearch(int no) {
		if(this.id == no) {
			return this;
		}
		HeroNode resNode = null;
		if(this.left != null) {
			resNode = this.left.preOrderSearch(no);
		}
		if(resNode != null) {
			return resNode;
		}
		if(this.right != null) {
			resNode = this.right.preOrderSearch(no);
		}
		return resNode;
	}

	public HeroNode midOrderSearch(int no) {
		HeroNode resNode = null;
		if(this.left != null) {
			resNode = this.left.midOrderSearch(no);
		}
		if(resNode != null) {
			return resNode;
		}
		if(this.id == no) {
			return this;
		}

		if(this.right != null) {
			resNode = this.right.midOrderSearch(no);
		}
		return resNode;
	}
	public HeroNode postOrderSearch(int no) {
		HeroNode resNode = null;
		if(this.left != null) {
			resNode = this.left.postOrderSearch(no);
		}
		if(resNode != null) {
			return resNode;
		}

		if(this.right != null) {
			resNode = this.right.postOrderSearch(no);
		}
		if(resNode != null) {
			return resNode;
		}
		if(this.id == no) {
			return this;
		}
		return resNode;
	}


}

```
