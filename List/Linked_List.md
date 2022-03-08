- 동적할당으로 데이터를 저장하는 방법
- 단순 연결 리스트에서는 데이터를 가지고 있는 공간인 Node 와 그 다음 주소를 저장하는 공간인 next Node로 구성되어있고, Node 의 마지막 데이터 공간의 next Node에는 Null 값이 들어간다.


- 단점 : 링크드 리스트는 Node에 저장되어 있는 nextNode를 따라서 다음 저장된 값을 찾기 때문에 원하는 값의 위치를 찾기 위해서는, 처음부터 순차적으로 탐색해야하는 단점이 있다.


![image](https://user-images.githubusercontent.com/86946575/157189168-3e409560-db78-4765-9a9d-d28f254b8219.png)

```cpp
#include <iostream>

using namespace std;

//노드 struct 구현 (data값과 nextNode가 존재)
struct node {
	int data;
	node* nextNode;
};

//링크드 리스트 클래스 생성
class LinkedList {
private:
	node* head;
	node* tail;
public:
	LinkedList() {
		//head 와 tail의 포인터를 초기화;
		head = NULL;
		tail = NULL;
	}
	//첫번째의 node 추가
	void addFrontNode(int n);
	//마지막의 node 추가
	void addNode(int n);

	//node 삽입
	void insertNode(node* prevNode, int n);
	//node 삭제
	void deleteNode(node* prevNode);

	//첫번째 노드 가져오기
	node* getHead() {
		return head;
	}
	//LinkedList 출력
	void display(node* head);
};

//첫번째의 node 추가
void LinkedList::addFrontNode(int n) {
	node* temp = new node;
	//temp의 데이터는 n
	temp->data = n;

	//LinkedList가 비어있으면
	if (head == NULL) {
		//첫 node는 temp
		head = temp;
		//마지막 node는 temp
		tail = temp;
	}
	//LinkedList에 데이터가 있으면
	else {
		//temp의 nextNode는 head
		temp->nextNode = head;
		//head는 temp
		head = temp;
	}
}

//마지막의 node 추가
void LinkedList::addNode(int n) {
	node* temp = new node;

	//temp의 데이터는 n
	temp->data = n;
	//temp의 nextNode = NULL값
	temp->nextNode = NULL;

	//LinkedList가 비어있으면
	if (head == NULL) {
		//첫 node는 temp
		head = temp;
		//마지막 node는 temp
		tail = temp;
	}
	//LinkedList에 데이터가 있으면
	else {
		//현재 마지막 node의 nextNode는 temp
		tail->nextNode = temp;
		//마지막 node는 temp
		tail = temp;
	}
}

//node 삽입
void LinkedList::insertNode(node* prevNode,int n) {
	node* temp = new node;
	//temp의 데이터는 n
	temp->data = n;

	//temp의 nextNode 저장
	//(삽입 할 앞 node의 nextNode를 temp의 nextNode에 저장)
	temp->nextNode = prevNode->nextNode;
	
	//temp 삽입
	//temp앞의 node의 nextNode를 temp로 저장
	prevNode->nextNode = temp;
}

//node 삭제
void LinkedList::deleteNode(node* prevNode) {

	//삭제할 node를 temp에 저장
	//(삭제할 node의 1단계 전 node의 nextNode) 
	node* temp = prevNode->nextNode;

	//삭제할 node를 제외
	//(삭제할 node의 nextNode를 1단계 전 node의 nextNode에 저장)
	prevNode->nextNode = temp->nextNode;

	//temp 삭제
	delete temp;
}

//LinkedList 출력
void LinkedList::display(node* head) {
	if (head == NULL) {
		cout << "\n";
	}
	else {
		cout << head->data << " ";
		display(head->nextNode);
	}
	cout << endl;
}

//메인 함수
int main() {
	LinkedList a;
	a.addNode(1);
	a.addNode(2);
	a.addNode(3);
	cout << "1,2,3을 LinkedList에 추가\n";
	a.display(a.getHead());
	a.addFrontNode(0);
	a.insertNode(a.getHead()->nextNode->nextNode, 1);
	cout << "0을 첫번째에 추가, 1을 세번째에 추가\n";
	a.display(a.getHead());
	a.deleteNode(a.getHead()->nextNode);
	cout << "세번째 노드를 삭제\n";
	a.display(a.getHead());

}
```
