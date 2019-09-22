# DataStructure - Tree Basic

부모와 자식관계가 있는 계층 구조를 Tree라고 한다.

### 1. 용어

- root node: 부모가 없는 노드, 트리는 하나의 루트노드를 가진다.
- leaf node: 자식이 없는 말단 노드를 의미한다.
- Internal node: 말단 노드가 아닌 노드를 의미한다.
- edge: 노드를 연결하는 선을 의미한다.
- Sibling: 같은 부모를 가지고 있는 노드들의 관계를 의미한다.
- Size: 자신을 포함한 모든 자손 노드의 개수를 의미한다.
- Depth: 루트에서 특정 노드에 도달하기 위해 거쳐야하는 edge의 수를 의미한다.
- Level: 노드의 높이, 특정 깊이를 가지는 노드의 집합을 의미한다.
- Degree: 하위 트리개수 / 간선(edge)수 즉, 각 노드가 지닌 가지의 수를 의미한다.
- degree of tree: 트리의 최대 degree를 의미한다.
- Height: 루트 노트에서 가장 깊이 떨어진 노드의 깊이를 의미한다.

### 2. 종류

- Binary Tree: child node가 최대 2개 까지만 있는 트리
  - Binary Search Tree: 특정 노드의 왼쪽 자식 노드와 자손들은 해당 노드보다 크기가 작고, 오른쪽 자식 노드와 자손들은 해당 노드보다 크기가 크다.
  - Complete Binary Tree: 모든 Sub Tree의 레벨이 갖고 마지막 레벨의  노드들이 왼쪽 자식노드부터 채워져 있으면 Complete Binary Tree라고 한다.
  - Full Binary Tree: 자식노드를 2개 모두가지고 있거나 아예 안가지고 있는 노드들로 이루어진 트리
  - Perfect Binary Tree: 모든 노드들이 2개의 자식노드를 가지고 있는 트리
- Ternary Tree: child node가 최대 3개 까지만 있는 트리
- Tries Tree: 문장 검색을 위해 트리에 Character을 저장하여 순회하는 트리
- Tree: 모든 트리들을 의미

### 3. Binary Tree 3가지 순회방법

- Inorder : Left > Root > Right
- Preorder: Root > Left > Right
- Postorder: Left > Right > root

( 구현 )

```java 
public class TreeTraversal {

	static TreeNode treeNodes[];

	static void preOrder(int n) {
		
		if(n== -1) return;
			
		TreeNode tr = treeNodes[n];
		System.out.print(n+ " ");
		preOrder(tr.left);
		preOrder(tr.right);
	}
	
	static void inOrder(int n) {
		
		if(n== -1) return;
			
		TreeNode tr = treeNodes[n];
		inOrder(tr.left);
		System.out.print(n+ " ");
		inOrder(tr.right);
	}
	
	static void postOrder(int n) {
		
		if(n== -1) return;
			
		TreeNode tr = treeNodes[n];
		postOrder(tr.left);
		postOrder(tr.right);
		System.out.print(n+ " ");
	}
	
	
	static class TreeNode{

		int left;
		int right;
		
		public TreeNode( int left, int right) {
			super();
			this.left = left;
			this.right = right;
		}
		
	}

}
```

