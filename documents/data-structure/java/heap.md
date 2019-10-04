# DataStructure - Heap



### 1. Heap 이란?

Heap이란 완전 이진 트리 구조로 다음과 같이 두가지 종류를 가지고 있다.

- **Max-Heap** : 항상 부모 노드가  자식 노드보다 큰 경우를 말 한다. root 노드는 tree에서 가장 작을 값을 가진다.
- **Min-Heap**: 항상 부모 노드가 자식 노드보다 작은 경우를 말 한다. root 노드는 tree에서 가장 큰 값을 가진다.

### 2. Heap Insert 

*Max Heap 기준으로 설명*

heap 에 새로운 값을 입력 할 경우 우선 트리의 마지막에 해당 값을 넣는다 그 이후 부모 노드와 비교하면서 해당 노드가 부모노드의 값과 큰지 비교하며 값이 크다면 부모노드와 위치를 바꿔 준다 이 런식으로  부모노드 보다 값이 작을 때 까지  반복하며 root에 도달 하였을 경우에는 return 해준다. 

트리의 높이에 따라 계속 부모노드와 비교 해주므로 heap의 insert 는 **log N** 의 시간이 걸린다.

### 3. Heap remove

*Max Heap 기준으로 설명*

heap에서 값을 삭제 할 경우, root노드를 삭제 한 후 해당 자리에 마지막 노드의 값을 넣어 준다. 그 이후 해당 값과 자식 노드의 값을 비교하여  값이 작다면 위치를 바꿔 준다. 해당 노드가 자식노드보다 값이 클때까지 반복해주며 트리의 끝에 도달했을 경우 return 해준다.

트리의 높이에 따라 계속 자식노드와 비교 해주므로 heap의 remove는  **log N** 의 시간이 걸린다.

### 4. Heap 노드 Index

Heap의 구현은 보통 **Array**형식으로 구현 되며 루트노드의 index 가 1일 경우 왼쪽 자식 의 index는 **(부모 index) * 2** 오른쪽 자식의 index는 **(부모 index)*2+1** 이다.

### 5. Java 로 구현

```java 
class MyHeap {
	int max = 100;
	int data[] = new int[max];
	int len = 1;

	public void push(int n) {
		data[len++] = n;
		
		int idx = len-1;
		while(idx > 1) {
			//해당 노드가 부모노드 보다 우선순위가 높다면 교체
			if(data[idx] < data[idx/2]) {
				int temp = data[idx];
				data[idx] = data[idx/2];
				data[idx/2] = temp;
			}
			else break;
			
			idx = idx/2;
		}
	}
	
	public void pop() {
		
		data[1] = data[--len];
		data[len] = 0;
		
		int inx = 1;
		
		while(true) {

			//1. 자식들 중에서 우선순위가 높은 친구를 알아내자
			//2. 나와 그 우선순위가 높은 친구를 비교해서 자리를 바꾸자
			
			int pIdx = -1; //우선순위가 높은 친구의 노드의 번호
			
			
			//(A) 자식이 모두 없는 경우
			//(B) 왼쪽 자식만 있는 경우
			//(C) 왼쪽 자식 오른쪽 자식 모두 존재하는 경우 
			
            //A
            if(len<= inx*2) break; 
			
      //B
			if(1<= inx*2 && inx*2 <len && len <= inx*2+1) {
				pIdx = inx*2;
			} 
      
      //C
			if(data[inx*2] < data[inx*2+1]) {
				pIdx = inx*2;
			}else {
				pIdx = inx*2+1;
			}
			
			if(data[inx] > data[pIdx]) {
				int temp = data[inx];
				data[inx]= data[pIdx];
				data[pIdx] = temp;
				inx = pIdx;
			}else break;
		}
	}
	
	public int top() {

		return data[1];
	}
	
}
```

