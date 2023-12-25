# 스택과 큐

## 1. 자료 구조

### 선형 구조

- 자료를 구성하는 데이터를 순차적으로 나열한 형태
- 스택, 큐, 배열, 연결 리스트

### 비선형 구조

- 하나의 데이터 뒤에 여러 개의 데이터가 존재할 수 있는 형태
- 트리, 그래프

![stack_1.png](..%2Fimg%2Fstack_1.png)

## 2. 스택

### 정의

- 데이터를 쌓아 올리는 형태의 자료구조
- 스택 상단(top) : 스택에서 입력이 이루어지는 부분
- 요소(element) : 스택에 저장되는 것
- 포화 스택 : 포화 상태의 스택, 풀스택
- 
![stack_2.png](..%2Fimg%2Fstack_2.png)

### 특징

- 후입선출(First-In Last-Out), 가장 먼저 입력된 데이터가 가장 나중에 출력
- 입력과 출력이 한쪽(TOP)에서만 실행

### 연산

- top() : 최상단 데이터 값 반환
- push() : 데이터 삽입
- pop() : 데이터 삭제하여 반환
- isempty() : 스택에 원소가 없으면 True, 있으면 False 반환
- isfull() : 스택에 원소가 없으면 False, 있으면 True 반환

### 활용 예시

- ‘뒤로 가기’ 혹은 ‘되돌리기’ 기능
- 깊이 우선 탐색(DFS) 구현
- 시스템 스택의 함수 호출 : 함수의 실행이 끝나면 자신을 호출한 함수로 복귀. 이 때 스택은 복귀할 주소를 기억하는 데 사용. 함수는 호출된 역순으로 되돌아가야 하기 때문

![stack_3.png](..%2Fimg%2Fstack_3.png)

## 3. 스택의 구현

### 1. 정적 구현 : 1차원 배열 사용

push와 pop할 때는 해당 위치를 알고 있어야 하므로 기억하고 있는 '스택 포인터(SP)'가 필요함

스택 포인터는 다음 값이 들어갈 위치를 가리키고 있음 (처음 기본값은 -1)

```java
private int sp = -1;
```

**push()**

```java
public void push(Object o) {
    if(isFull(o)) {
        return;
    }
    
    stack[++sp] = o;
}
```

스택 포인터가 최대 크기와 같으면 return

아니면 스택의 최상단에 값을 넣음

**pop()**

```java
public Object pop() {
    
    if(isEmpty(sp)) {
        return null;
    }
    
    Object o = stack[sp--];
    return o;
    
}
```

스택 포인터가 0이 되면 null로 return;

아니면 스택의 최상단 값을 꺼내옴

**isEmpty()**

```java
private boolean isEmpty(int cnt) {
    return sp == -1 ? true : false;
}
```

입력 값이 최초 값과 같다면 true, 아니면 false

**isFull()**

```java
private boolean isFull(int cnt) {
    return sp + 1 == MAX_SIZE ? true : false;
}
```

스택 포인터 값+1이 MAX_SIZE와 같으면 true, 아니면 false

**정적 배열 스택의 단점**

- **최대 크기가 고정되어 있어서 스택이 가득 차는 경우가 발생**
- **동적 배열 스택이나 연결 리스트 구현으로 해결**

### 동적 배열로 구현

위처럼 구현하면 스택에는 MAX_SIZE라는 최대 크기가 존재해야 한다

(스택 포인터와 MAX_SIZE를 비교해서 isFull()로 비교하기 때문)

```java
public void push(Object o) {
    
    if(isFull(sp)) {
        
        Object[] arr = new Object[MAX_SIZE * 2];
        System.arraycopy(stack, 0, arr, 0, MAX_SIZE);
        stack = arr;
        MAX_SIZE *= 2; // 2배로 증가
    }
    
    stack[sp++] = o;
}
```

1. 기존 스택의 2배 크기만큼 임시 배열(arr)을 만들고
2. arraycopy를 통해 stack의 인덱스 0부터 MAX_SIZE만큼을 arr 배열의 0번째부터 복사
3. 복사 후에 arr의 참조 값을 stack에 덮어 씌움
4. 마지막으로 MAX_SIZE의 값을 2배로 증가

   이러한 방식으로 스택이 가득 차면, 자동으로 확장되는 스택을 구현할 수 있음


### 연결 리스트로 구현

단점 : 구현이 복잡하고 삽입/삭제 시간이 오래 걸림

```java
public class Node {

    public int data;
    public Node next;

    public Node() {
    }

    public Node(int data) {
        this.data = data;
        this.next = null;
    }
}
```

```java
public class Stack {
    private Node head;
    private Node top;

    public Stack() {
        head = top = null;
    }

    private Node createNode(int data) {
        return new Node(data);
    }

    private boolean isEmpty() {
        return top == null ? true : false;
    }

    public void push(int data) {
        if (isEmpty()) { // 스택이 비어있다면
            head = createNode(data);
            top = head;
        }
        else { //스택이 비어있지 않다면 마지막 위치를 찾아 새 노드를 연결시킨다.
            Node pointer = head;

            while (pointer.next != null)
                pointer = pointer.next;

            pointer.next = createNode(data);
            top = pointer.next;
        }
    }

    public int pop() {
        int popData;
        if (!isEmpty()) { // 스택이 비어있지 않다면!! => 데이터가 있다면!!
            popData = top.data; // pop될 데이터를 미리 받아놓는다.
            Node pointer = head; // 현재 위치를 확인할 임시 노드 포인터

            if (head == top) // 데이터가 하나라면
                head = top = null;
            else { // 데이터가 2개 이상이라면
                while (pointer.next != top) // top을 가리키는 노드를 찾는다.
                    pointer = pointer.next;

                pointer.next = null; // 마지막 노드의 연결을 끊는다.
                top = pointer; // top을 이동시킨다.
            }
            return popData;
        }
        return -1; // -1은 데이터가 없다는 의미로 지정해둠.

    }

}
```

# 큐

## 4. 큐

### 정의

- 데이터가 입력된 순서대로 처리하는 형태의 자료구조
- 
![stack_4.png](..%2Fimg%2Fstack_4.png)

### 특징

- 선입선출(First-In First-Out), 가장 먼저 입력된 데이터가 가장 먼저 출력
- Front : 데이터의 삭제 및 출력이 이루어지는 곳, 첫 원소
- Rear : 데이터가 삽입되는 곳, 마지막 원소

### 연산

- enqueue() : 데이터 삽입
- dequeue() : 데이터 삭제하여 반환
- isempty() : 큐가 비어있는지 확인
- isfull() : 큐가 원소로 꽉 차있는지 확인

### 활용 예시

- 버퍼
- 너비 우선 탐색(BFS)

## 5. 큐의 구현

### 일반 큐 구현

데이터를 넣고 뺄 때 해당 값의 위치를 기억해야 함. (스택에서 스택 포인터와 같은 역할)

front : dequeue 할 위치 기억, rear : enqueue 할 위치 기억

```java
private int size = 0; 
private int rear = -1; 
private int front = -1;

Queue(int size) { 
    this.size = size;
    this.queue = new Object[size];
}
```

**enqueue()**

```java
public void enqueue(Object o) {
    
    if(isFull()) {
        return;
    }
    
    queue[++rear] = o;
}
```

enqueue 시, 가득 찼다면 꽉 차 있는 상태에서 enqueue를 했기 때문에 overflow

아니면 rear에 값 넣고 1 증가

**dequeue()**

```java
public Object dequeue(Object o) {
    
    if(isEmpty()) { 
        return null;
    }
    
    Object o = queue[front];
    queue[front++] = null;
    return o;
}
```

dequeue를 할 때 공백이면 underflow

front에 위치한 값을 object에 꺼낸 후, 꺼낸 위치는 null로 채워줌

**isEmpty()**

```java
public boolean isEmpty() {
    return front == rear; // front와 rear가 같아지면 비어진 것
}
```

**isFull()**

```java
public boolean isFull() {
    return (rear == queueSize-1); // rear가 사이즈-1과 같아지면 가득찬 것
}
```

**일반 큐의 단점**

- **큐에 빈 메모리가 남아 있어도, 꽉 찬 것으로 판단할 수도 있음(rear가 끝에 도달했을 때)**
- **원형 큐로 논리적으로 배열의 처음과 끝이 연결되어 있는 것으로 간주**

### 원형 큐 구현

원형 큐는 초기 공백 상태일 때 front와 rear가 0

공백, 포화 상태를 쉽게 구분하기 위해 **자리 하나를 항상 비워둠**

(index + 1) % size로 순환시킨다

```java
private int size = 0; 
private int rear = 0; 
private int front = 0;

Queue(int size) { 
    this.size = size;
    this.queue = new Object[size];
}
```

**enqueue()**

```java
public void enqueue(Object o) {
    
    if(isFull()) {
        return;
    }
    
    rear = (++rear) % size;
    queue[rear] = o;
}
```

enqueue 시, 가득 찼다면 꽉 차 있는 상태에서 enqueue를 했기 때문에 overflow

**dequeue()**

```java
public Object deQueue(Object o) {
    
    if(isEmpty()) { 
        return null;
    }
    
    preIndex = front;
    front = (++front) % size;
    Object o = queue[preIndex];
    return o;
}
```

dequeue를 할 때 공백이면 underflow

**isEmpty()**

```java
public boolean isEmpty() {
    return front == rear; // front와 rear가 같아지면 비어진 것
}
```

**isFull()**

```java
public boolean isFull() {
    return ((rear+1) % size == front); // (rear + 1) % size가 front와 같으면 가득찬 것
}
```

**원형 큐의 단점**

- **메모리 공간은 잘 활용하지만, 배열로 구현되어 있기 때문에 큐의 크기가 제한**

### 연결리스트 큐 구현

크기가 제한이 없고 삽입, 삭제가 편리

**enqueue()**

```java
public void enqueue(E item) {
    Node oldlast = tail; // 기존의 tail 임시 저장
    tail = new Node; // 새로운 tail 생성
    tail.item = item;
    tail.next = null;
    if(isEmpty()) head = tail; // 큐가 비어있으면 head와 tail 모두 같은 노드 가리킴
    else oldlast.next = tail; // 비어있지 않으면 기존 tail의 next = 새로운 tail로 설정
}
```

- 데이터 추가는 끝 부분인 tail에 한다
- 기존의 tail는 보관하고, 새로운 tail 생성
- 큐가 비었으면 head = tail을 통해 둘이 같은 노드를 가리키도록 함
- 큐가 비어있지 않으면, 기존 tail의 next에 새로 만든 tail을 설정

**dequeue()**

```java
public T dequeue() {
    // 비어있으면
    if(isEmpty()) {
        tail = head;
        return null;
    }
    // 비어있지 않으면
    else {
        T item = head.item; // 빼낼 현재 front 값 저장
        head = head.next; // front를 다음 노드로 설정
        return item;
    }
}
```

- 데이터는 head로부터 꺼낸다
- (가장 먼저 들어온 것부터 빼야하므로)head의 데이터를 미리 저장
- 기존의 head를 그 다음 노드의 head로 설정
- 저장해둔 데이터를 return

이처럼 삽입은 tail, 제거는 head로 하면서 삽입/삭제를 스택처럼 O(1)에 가능하도록 구현이 가능하다.

## 참고자료

[[자료구조] 자료구조란?(선형구조, 비선형구조)](https://osy0907.tistory.com/84)

[[자료구조] 4. 스택(Stack)이란? / 연산, 구현방법](https://roi-data.com/entry/자료구조-4-스택Stack이란-연산-구현방법)

[자료구조 - 큐(Queue)란?](https://galid1.tistory.com/483)

[[자료구조] 스택(Stack)과 큐(Queue)](https://dev-records.tistory.com/entry/자료구조-스택Stack과-큐Queue)

[Git: Songwonseok/CS-Study/Stack & Queue.md](https://github.com/Songwonseok/CS-Study/blob/main/DataStructure/Stack%20%26%20Queue.md)