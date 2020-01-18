#线索化二叉树

描述待添加

####代码
```java
public class ThreadedBinaryTreeDemo {
	public static void main(String[] args) {
		Node2 root = new Node2(1, "root");
		Node2 node2 = new Node2(3, "node2");
		Node2 node3 = new Node2(6, "node3");
		Node2 node4 = new Node2(8, "node4");
		Node2 node5 = new Node2(10, "node5");
		Node2 node6 = new Node2(14, "node6");

		//手动创建
		root.setLeft(node2);
		root.setRight(node3);

		node2.setLeft(node4);
		node2.setRight(node5);

		node3.setLeft(node6);

		BinaryTree2 bt = new BinaryTree2();
		bt.setRoot(root);
		bt.threadNodes();

		//测试
		System.out.println(node5.getLeft());
		System.out.println(node5.getRight());

	}


}
//线索化二叉树
class BinaryTree2 {
	private Node2 root;
	// 为了线索化建立当前节点的前驱节点
	private Node2 pre = null;

	//遍历中序线索化二叉树
	public void threadList() {
		Node2 node = root;
		while(node != null) {
			//找lefttype == 1的节点
			while(node.getLeftType() == 0) {
				node = node.getLeft();
			}
			System.out.println(node);
			while(node.getRightType() == 1) {
				node = node.getRight();
				System.out.println(node);
			}
			node = node.getRight();
		}
	}

	//重载线索化二叉树方法
	public void threadNodes() {
		this.threadNodes(root);
	}

	public void threadNodes(Node2 node) {

		// 如果node为空
		if (node == null) {
			return;
		}
		// (1)先线索化左子树
		threadNodes(node.getLeft());
		// (2)线索化当前节点

		// 处理当前节点前驱节点
		if (node.getLeft() == null) {
			node.setLeft(pre);
			node.setLeftType(1);
		}
		// 处理后继节点
		if (pre != null && pre.getRight() == null) {
			pre.setRight(node);
			pre.setRightType(1);
		}
		// 让当前节点变成下一个节点的前驱节点
		pre = node;
		// (3)再线索化右子树
		threadNodes(node.getRight());


	}

	public Node2 getPre() {
		return pre;
	}

	public void setPre(Node2 pre) {
		this.pre = pre;
	}

	public void delNode(int no) {
		if (root != null) {
			if (root.getId() == no) {
				root = null;
			}
		} else {
			System.out.println("空！");
		}
	}

	public void setRoot(Node2 root) {
		this.root = root;
	}

	public void preOrder() {
		if (root != null) {
			this.root.preOrder();
		} else {
			System.out.println("树空");
		}
	}

	public void mideOrder() {
		if (root != null) {
			this.root.midOrder();
		} else {
			System.out.println("树空");
		}
	}

	public void postOrder() {
		if (root != null) {
			this.root.postOrder();
		} else {
			System.out.println("树空");
		}
	}

	public Node2 preOrderSearch(int no) {
		if (root != null) {
			return root.preOrderSearch(no);
		} else {
			System.out.println("树空");
			return null;
		}
	}

	public Node2 midOrderSearch(int no) {
		if (root != null) {
			return root.midOrderSearch(no);
		} else {
			System.out.println("树空");
			return null;
		}
	}

	public Node2 postOrderSearch(int no) {
		if (root != null) {
			return root.postOrderSearch(no);
		} else {
			System.out.println("树空");
			return null;
		}
	}
}
//加入线索化的节点
public class Node2 {
	private int id;
	private String name;
	private Node2 left;
	private Node2 right;
	private int leftType;
	private int rightType;
	//type == 0左子树  1前驱
	//type == 0右子树  1后继

	public void delNode(int no) {
		if(this.left != null &&this.left.id == no) {
			this.left = null;
			return;
		}

		if(this.right != null &&this.right.id == no) {
			this.right = null;
		}

		if(this.left != null) {
			this.left.delNode(no);
		}
		if(this.right != null) {
			this.right.delNode(no);
		}
	}



	public int getLeftType() {
		return leftType;
	}



	public void setLeftType(int leftType) {
		this.leftType = leftType;
	}



	public int getRightType() {
		return rightType;
	}



	public void setRightType(int rightType) {
		this.rightType = rightType;
	}



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
	public Node2 getLeft() {
		return left;
	}
	public void setLeft(Node2 left) {
		this.left = left;
	}
	public Node2 getRight() {
		return right;
	}
	public void setRight(Node2 right) {
		this.right = right;
	}
	public Node2(int id, String name) {
		super();
		this.id = id;
		this.name = name;
	}
	@Override
	public String toString() {
		return "Node2 [id=" + id + ", name=" + name + "]";
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

	public Node2 preOrderSearch(int no) {
		if(this.id == no) {
			return this;
		}
		Node2 resNode = null;
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

	public Node2 midOrderSearch(int no) {
		Node2 resNode = null;
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
	public Node2 postOrderSearch(int no) {
		Node2 resNode = null;
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
