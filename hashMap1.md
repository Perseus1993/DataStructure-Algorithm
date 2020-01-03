#HashTable

```java
public class Ht {

	public static void main(String[] args) {
		HashTable ht = new HashTable(7);

		String key = "";
		Scanner scanner = new Scanner(System.in);
		while(true) {
			System.out.println("add 添加");
			System.out.println("list 显示");
			System.out.println("exit 退出");
			key = scanner.next();
			switch(key) {
			case "add":
				System.out.println("输入id");
				int id = scanner.nextInt();
				System.out.println("输入名字");
				String name = scanner.next();
				Emp emp = new Emp(id, name);
				ht.add(emp);
				break;
			case "exit":
				scanner.close();
				System.exit(0);
			case "list":
				ht.list();
				break;
			case "find":
				System.out.println("输入id");
				int id2 = scanner.nextInt();
				ht.findEmpById(id2);
				break;
			default:
				break;

			}
		}

	}


}
class HashTable{
	private EmpLinkedList[] empLinkedListArray;
	private int size;
	public HashTable(int size) {
		this.size = size;
		empLinkedListArray = new EmpLinkedList[size];
		for(int i = 0; i < size; i++) {
			empLinkedListArray[i] = new EmpLinkedList();
		}

	}
	public void add(Emp emp) {
		int empLinkedListNo = hashFun(emp.id);
		empLinkedListArray[empLinkedListNo].add(emp);
	}
	public void list() {
		for(int i = 0; i < size; i++) {
			empLinkedListArray[i].list(i);
		}
	}
	public void findEmpById(int id) {
		int empLinkedListNO = hashFun(id);
		Emp emp = empLinkedListArray[empLinkedListNO].findEmpById(id);
		if(emp != null) {
			System.out.printf("在%d条链表中 找到雇员， id =%d \n",empLinkedListNO, id);

		}else {
			System.out.println("没有啊");

		}
	}

	public int  hashFun(int id) {
		return id % size;
	}
}

class Emp{
	public int id;
	public String name;
	public Emp next;
	public Emp(int id, String name) {
		super();
		this.id = id;
		this.name = name;
	}
}

class EmpLinkedList{
	private Emp head;
	public void add(Emp emp) {
		if(head == null) {
			head = emp;
			return;
		}
		Emp curEmp = head;
		while(true) {
			if(curEmp.next == null) {
				break;
			}
			curEmp = curEmp.next;

		}
		curEmp.next = emp;
	}

	public void list(int no) {
		if(head == null) {
			System.out.println("第" + (no + 1) + "链表为空");
			return;
		}
		System.out.println("第" + (no + 1) + "链表为");
		Emp curEmp = head;
		while(true) {
			System.out.printf("id=%d name=%s\t", curEmp.id, curEmp.name);
			if(curEmp.next == null) {
				break;
			}
			curEmp = curEmp.next;
		}
		System.out.println();
	}
	public Emp findEmpById(int id) {
		if(head == null) {
			System.out.println("空");
			return null;
		}
		Emp curEmp = head;
		while(true) {
			if(curEmp.id == id) {
				break;
			}
			if(curEmp.next == null) {
				curEmp = null;
				break;
			}
			curEmp = curEmp.next;
		}
		return curEmp;
	}
}
```
