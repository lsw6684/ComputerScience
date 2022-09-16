<p align="center" style="font-size:50px">
    <a href="https://github.com/lsw6684/ComputerScience">HOME</a>
</p>

___

<br />

# Interview
- [Data Structure](#data-structure)
- [Java](#java)
- [Operating System](#operating-system)
---
## Data Structure
### Array는 어떤 자료구조인가요?
Array는 연관된 data를 메모리상에 연속적이며 순차적으로, 미리 할당된 크기만큼 저장하는 자료구조입니다.

<br />

#### Array의 특징은 어떤 것들이 있나요?
대표적으로 **고정된 저장 공간**과 **순차적 데이터 저장**이 있습니다. 

Array의 **장점**은 lookup과 append가 빠르다는 것입니다. 따라서 조회를 자주 해야되는 작업에서 사용됩니다.

**단점**으로는, fixed-size 특성상 선언 시에 크기를 미리 지정해야 된다는 것입니다. 이는 메모리 낭비나 Overhead가 발생할 수 있습니다.

<br />

#### 시간 복잡도

|Array||
|:---|:---|
|access|O(1)|
|append|O(1)|
|마지막 원소 delete|O(1)|
|insertion|O(n)|
|deletion|O(n)|
|search|O(n)|

<br />

#### 미리 예상한 것보다 더 많은 수의 data를 저장하느라 Array의 size를 넘어서게 됐습니다. 이 때, 어떻게 해결할 수 있을까요?
기존 size보다 더 큰 Array를 선언하여, 데이터를 옮기고 기존 Array를 삭제합니다. 이와 같이 동적으로 배열의 크기를 조절하는 자료구조를 Dynamic array라고 합니다. 

size를 예측하기 쉽지 않다면, Array 대신 Linked List를 사용함으로써, 데이터가 추가될 때마다 메모리 공간을 할당받는 방식을 사용합니다.

***

### Dynamic Array는 어떤 자료구조인가요?
Array의 경우 size가 고정되었기 때문에 선언 시에 설정한 size보다 많은 갯수의 data를 저장할 수 없습니다. 하지만, Dynamic Array는 저장 공간이 가득 차면, **resize**를 통해 유동적으로 size를 조절하여 데이터를 저장하는 자료구조입니다.

<br />

#### Dynamic Array의 resize를 설명해 보세요.
resizing을 하는 방법은 여러 가지가 있는데, 대표적으로 기존 Array size의 2배 를 할당하는 **doubling**이 있습니다. 데이터 append 시 O(1)의 시간복잡도를 가지다가, doubling이 발생하면, 데이터를 일일이 옮겨야 하므로 O(n)의 시간복잡도를 가집니다. 

- 분할상환 시간복잡도 Amortized time complexity
    ```
    append 시 O(1)로 진행 되다가 doubling이 발생할 때만 O(n)이 됩니다. 이러한 경우 시간 복잡도를 O(1)로 규정하며, 더욱 정확히 표현하면 amortized O(1)이라고 칭합니다.
    ```

<br />

#### Dynamic Array를 Linked List와 비교하여 장단점을 설명해 주세요
**Linked List와 비교했을 때, Dynamic Array의 장점**은
- 데이터 접근과 할당이 O(1)로 굉장히 빠른 속도를 자랑합니다. Random access의 index 접근 방법이 배열 첫 data의 주소값에 offset을 더하는 산술 연산으로 이루어져 있기 때문입니다. 
- Dynamic Array의 맨 뒤에 데이터를 추가하거나 삭제하는 것이 O(1)의 시간 복잡도이며 상대적으로 빠릅니다.

**Linked List와 비교했을 때, Dynamic Array의 단점**은
- Dynamic Array의 맨 끝이 아닌 곳에 data를 insert하거나 remove할 때, O(n)의 시간복잡도로 느린 편입니다. 메모리상에서 data들이 연속적으로 저장되어 있으므로, 이후의 data들을 모두 한 칸씩 shift 해야하기 때문입니다.
- resize를 해야할 때, 현저히 낮은 performance가 발생합니다.
- resize 시 필요 이상의 메모리 공간을 할당받기 때문에, 낭비되는 메모리 공간이 발생합니다.

***

### Linked List에 관해서 설명해 주세요.
Node라는 구조체로 이루어져 있는데, Node는 데이터 값과 다음 Node의 address로 구성됩니다. Linked List는 **물리적인 메모리상에서는 비연속적으로 저장** 되지만, 각각의 Node가 다음 Node의 address를 가리킴으로써 **논리적인 연속성을 가진 자료구조**입니다.

메모리 할당이 데이터 추가 시 이루어지기 때문에, 메모리를 좀 더 효율적으로 사용할 수 있으며 물리적 연속성을 유지하지 않아도 되는 이유로 메모리 사용이 자유로운 대신, Next address를 추가적으로 저장해야 하기 때문에 데이터 하나당 차지하는 메모리가 더 커지게 됩니다.

#### 시간 복잡도

|Linked List||
|:---|:---|
|access|O(n)|
|search|O(n)|
|insertion|O(1)|
|deletion|O(1)|

#### Linked List를 Array와 비교하여 설명해 주세요.
Array와 다르게 Linked List는 물리적 메모리상으로 연속적이지 않지만, 메모리 주소값을 저장함으로써 논리적 연속성을 띕니다. 저장할 데이터의 크기를 모르는 상태에서 Array보다 좋은 performance를 발휘하며 삽입, 삭제가 빈번한 상황에서 권장됩니다.

***

### Queue는 어떤 자료구조인가요?
선입선출 FIFO(First In First Out)의 자료구조입니다. 시간복잡도는 enqueue, dequeue 모두 O(1)이며 활요 예시로는 Cache, 프로세스 관리, 너비우선탐색(BFS) 등이 있습니다.
- Array-Based Queue : enqueue와 dequeue과정에서 남는 메모리가 발생하는 이유로, 낭비를 줄이기 위해 Circular queue 형식으로 구현합니다.
- List-Based Queue: 재 할당이나 메모리 낭비 걱정을 할 필요가 없습니다.
- Deque(Double Ended Queue) : 양 방향으로 enqueue/dequeue가 가능합니다.
- Priority queue : 삽입 순이 아닌 우선순위로 enqueue/dequeue가 가능합니다.

#### Queue 구현 시 Array-Base와 List-Base에 어떤 차이가 있나요?
**Array-Base**는 메모리 낭비를 줄이기 위해 Circular queue로 구현하는 것이 일반적입니다. fixed size를 넘어간 상태에서 enqueue가 발생하면, Dynamic Array와 같은 방법으로 Array size를 확장시켜야 하지만, 시간복잡도는 amortized O(1)을 유지할 수 있습니다.

**List-Base**는 보통 singly-linked list로 구현합니다. enqueue는 단순히 singly-linked list에서 append 하는 것으로 구현되며 dequeue는 맨 앞의 원소를 제거하고 first head를 변경하면 되기 떄문에 모두 O(1)로 가능합니다.

두 방법 모두 O(1)의 시간복잡도를 갖습니다. Array-Base의 경우 전반적으로 performance가 더 좋지만, worst case의 경우 resize로 인해 더욱 느릴 수 있습니다. List-Base는 enqueue 발생 시 마다 meomory allocation을 해야 하기 때문에 전반적인 runtime이 느릴 수 있습니다.

#### Queue와 Priority Queue를 비교하여 설명해 주세요.
Queue는 FIFO구조이며 Priority Queue는 들어간 순서에 상관 없이 우선순위가 높은 데이터가 먼저 나옵니다. Queue의 시간복잡도는 enqueue/dequeue 모두 O(1)이며, Priority queue는 Heap 자료구조로 O(log n)입니다.

#### Heap이 어떤 자료구조인지 설명해 주실래요?
Heap은 그 자체로 우선순위큐 구현과 일치합니다. 완전이진트리 구조로 Max Heap과 Min Heap으로 구분됩니다. Max힙을 예로 들자면, 각 child node의 값은 parent node보다 작아야 하며 root node에 저장된 값이 가장 큰 값이 됩니다.  

***

### Stack은 어떤 자료구조인가요? 
후입선출 LIFO(Last In First Out)의 자료구조입니다. push, pop 모두 O(1)이며 후위 표기법 연산, 괄호 유효성 검사, 웹 브라우저 방문기록(뒤로 가기), DFS 등이 있습니다.

***

### 트리 자료구조에 대해 설명해 주세요
노드와 간선들로 이루어진 자료구조로, 사이클이 없는 자료구조입니다. 즉, 루트에서 한 노드로 가는 경로는 유일합니다.

<br />

#### 트리와 그래프의 차이가 무엇인가요?
사이클의 유무입니다. 그래프는 트리와 같이 노드, 간선으로 이루어진 자료구조로 방향과 무방향이 존재하며, 트리는 그래프의 한 종류로써 방향성 있는 비순환 그래프입니다.

***

### BST는 어떤 자료구조인가요?
이진 탐색트리는 정렬된 tree입이니다. 어느 node를 선택하든 해당 node의 left subtree에는 그 node 값보다 작은 값들을 지닌 node로만 이루어져 있습니다. 그리고 right subtree에는 그 node의 값보다 큰 값들을 지닌 node로만 이루어져 있는 O(log n)의 binary tree입니다.

BST는 저장과 동시에 정렬을 하는 자료구조로, 노드들을 바닥에 투영 시 오름차순 정렬 된다는 것을 알 수 있습니다.

<br />

#### 이진트리(Binary tree)는 어떤 자료구조인가요?
모든 node의 child nodes의 갯수가 2 이하인 트리를 이진트리라고 합니다.

<br />

#### BST의 worst case의 시간복잡도는 어떻게 되며, 어떤 경우에 발생하나요?
O(n)이며, 균형 없이 한 쪽으로 치우친 tree의 경우 발생합니다. Linked List와 다를 게 없어진다고 볼 수 있습니다.

해결 방법으로는 자가 균형 이진 탐색 트리(Self-Balancing BST)가 있습니다. 이진 트리의 균형을 유지하며, 대표적으로 AVL트리와 Red-Black Tree가 있습니다. Java에서는 hashmap의 sepaerate chaining으로써 Linked List와 Red-Black Tree를 병행하여 저장합니다.
- AVL Tree : 균형도를 사용하여 삽입/삭제 시 균형을 맞춥니다. **균형도가 절댓값 2 미만이면 균형 트리이며, 2 이상이면 불균형 트리**입니다.
    - leaf노드의 높이는 항상 0
    - 자식이 한 개만 있으면 없는 쪽은 -1로 계산(null node)
    - 부모 노드 높이 = Max(좌측 노드 높이, 우측 노드 높이) + 1
    - **균형도** = 좌측 노드 높이 - 우측 노드 높이
        - 균형도가 양수 : 좌측 서브 트리가 비대
        - 균형도가 음수 : 우측 서브 트리가 비대
- Red-Black Tree :
    - 모든 노드는 red, black으로 구성
    - 루트 노트는 black
    - nil 노드는 black : nil 노드는 존재하지 않음을 의미하며 자녀가 없을 때 자녀를 nil노드로 표기함으로써 값이 있는 노드와 동등하게 취급합니다. **RB트리에서 leaf노드는 nil노드**로 계산합니다.
    - red의 자녀들은 black, red는 연속일 수 없습니다.
    - 임의의 노드에서 자손 nil 노드들 까지 가는 경로들에서 **black**의 수는 같습니다.
    - black height : 노드 x에서 임의의 자손 nill 노드까지 내려가는 경로에서의 black 수.
***

### Hash table은 어떤 자료구조인가요?
효율적인 탐색(빠른 탐색)을 위한 자료구조로 key-value쌍의 데이터를 입력받습니다. hash function h에 key값을 입력하여 얻은 해시값 h(k)를 위치로 지정하여 key-value 데이터 쌍을 저장합니다. 저장/삭제/검색 시간 복잡도는 모두 O(1)이며 해당 공간을 slot 또는 bucket이라고 합니다.
- Direct-address Table : 직접 주소화 테이블로 key값으로 k를 갖는 원소는 index k에 저장합니다. 불필요한 공간 낭비와 다양한 자료형을 담을 수 없게 된다는 단점이 있습니다.

<br >

#### Hash table에서 발생하는 Collision은 무엇이고 어떻게 해결할 수 있나요?
key의 해시값이 중복되는 경우를 말합니다. key가 다르더라도 해시값이 같을 수 있는데 이러한 collision이 적게 발생하고 연산속도가 빨라야 **좋은 hash function**이라고 할 수 있으며, 어쩔 수 없이 Collision이 발생한 경우 separate chaining이나 open addressing 등의 방식을 사용하여 해결합니다.
- separate chaining : Linked List를 사용하여 Collision 발생 시 노드(slot)를 추가하여 데이터를 저장합니다. 최악의 경우 O(n)이 발생할  수 있습니다.
- open addressing : Collision 발생 시 특정 규칙에 따라 hash table의 비어있는 slot을 찾습니다. 추가적인 메모리를 사용하지 않으므로, Linked List나 tree 자료구조를 사용하는 separate chaining방식에 비해 메모리를 적게 사용합니다. open addressing 방식은 찾는 방법에 따라 크게 Linear Probing, Quadratic Probing, Double Hashing으로 나뉩니다.
    - Linear Probing(선형 조사법) & Quadratic Probing(이차 조사법) : 선형 조사법은 충돌이 발생한 해시값으로 부터 일정 값만큼 건너 뛰어 빈 slot에 데이터를 저장하며 이차 조사법은 제곱수로 건너 뛰어 빈 slot을 찾아 데이터를 저장합니다.
        - 충돌 횟수가 많아지면 특정 영역에 데이터가 집중적으로 몰리는 클러스터링 현상이 발생하여 평균 탐색 시간이 증가하게 된다는 단점이 있습니다.
    - Double Hashing(이중해시, 중복해시) : Collision 시 open addressing 해결 방식 중 하나로, 클러스터링 문제가 발생하지 않도록 합니다. 최초의 해시값을 얻고 충돌 발생 시 또 다른 해시 함수를 이용합니다.

***

### 퀵소트에 대해 설명해주세요
1. 피벗을 선택합니다. (보통 첫 번째를 선택)
2. 오른쪽(j)에서 왼쪽으로 가면서 피벗보다 작은 수를 탐색합니다.
3. 왼쪽(i)에서 오른쪽으로 가면서 피벗보다 큰 수를 탐색합니다.
4. i와 j를 교환합니다.
5. 2 ~ 4 과정을 반복합니다.
6. i > j인 경우, 즉 더 이상 위 단계를 진행할 수 없으면, 현재 피벗과 i를 교환합니다.

<br />

#### 퀵소트의 시간복잡도는 무엇입니까?
평균 O(NlogN) 입니다.

<br />

#### 왜 평균이라는 표현을 쓰죠?
정렬된 경우 O(N<sup>2</sup>)의 시간복자도를 갖지만, 그 경우가 매우 미미하기 때문에 평균이라는 표현을 덧붙여 사용합니다.

***

## Java
### 중복을 허용하지 않는 자료구조 Set, Map의 경우, 내부적으로 동일하다는 것을 어떻게 알 수 있나요?
HashSet 기준으로 설명하면, HashSet은 내부적으로 HashMap을 가지고 있으며 HashSet의 `add()`, `addAll()` 메서드는 HashMap의 `put()` 메서드를 사용하고 있습니다. HashMap은 put() 메서드 사용 시 Object의 `equals()`를 사용함으로써 중복을 방지합니다.

<br />

#### Object의 `equals()`메서드를 언제 오버라이딩 하나요?
두 객체의 값을 비교할 때 `hashCode()`와 같이 오버라이딩 하여 동등성 비교를 진행합니다.
- 동일성 : 두 객체가 완전히 같은 경우. `==`, `주소가 같음`
- 동등성 : 두 객체의 내용이 같은 경우. `equals`, `값이 같음`

<br />

#### Object의 equals()메서드를 오버라이딩 할 때 hashCode()를 왜 같이 오버라이딩 하나요?
Object의 `equals()` 메서드는 객체의 주소값을 int 형으로 변환하여 반환하기 때문에 객체마다 서로 다른 값을 반환하여 동등성 비교를 수행합니다. 이에 따라 해시 자료구조 사용 시 데이터 중복 문제가 발생할 수 있으며, 자바 규약을 위반합니다.
- 데이터 중복 문제 : HashSet, HashMap 자료구조 사용 시 데이터가 중복되는 문제가 발생하는 것을 말합니다. 
    - A라는 클래스를 new 연산자로 b객체를 생성하고 HashMap에 저장합니다.
    - A라는 클래스르 다시 new 연산자로 c객체를 생성하고 HashMap에 저장하게 되면
    - 같은 클래스이므로 value값이 갱신되기를 기대하지만, 서로 다른 해시값을 가지므로 두 개의 키, 값이 저장되게 됩니다.
- 규약 위반
    - `equals()`메서드는 멱등성을 가져야 합니다. 
        - 멱등성 : 연산을 여러번 해도 결과는 달라지지 않음
    - `equals()` 비교 시 true를 리턴한다면, 두 객체의 hashCode값도 일치해야 합니다.

***

### for each(향상된 for문)를 사용할 수 있는 자료구조는 최종적으로 어떤 인터페이스를 상속받고 있나요?
Iterable 인터페이스를 상속받고 있습니다.

<br />

#### for each 사용 시 다음 데이터를 얻기 위해 내부적으로 호출되는 메서드에 대해 아나요?
Collection 인터페이스는 `Iterable` 인터페이스를 상속 받고 있기 때문에, `iterator()`메서드를 가지고 있고, 이 메서드는 `Iterator` 인터페이스를 반환합니다. 따라서 `Iterator`의 `hasNext()` 메서드로 다음 원소가 있는지 검사하고 `next()` 메서드 호출로 원소 추출 후 cursor값을 증가시킵니다.

<br />

#### `Iterable`와 `Iterator`의 차이는 무엇인가요?
`Iterable` 인터페이스는 `Iterator` 인터페이스를 반환하는 `Iterator()`메서드를 강제하여, `Iterable` 인터페이스를 상속, 구현하는 객체는 for-each를 사용할 수 있습니다.

`Iterator`인터페이스는 `hasNext()`, `next()`같은 메서드를 가지고 있고, `Iterator`인터페이스를 구현하는 객체가 이를 구현하여 Collection의 요소들을 순회하는 기능을 구현합니다.

***

### HashMap과 HashTable의 차이는 무엇인가요?
- HashMap
    - 동기화 지원하지 않음
    - 분리연결법을 사용
    - key에 null값 허용
    - 보조해시를 사용하기 때문에 해시 충돌 발생 가능성이 더 적음
- hashTable
    - 동기화를 지원하므로 멀티쓰레드 환경에서 Thread-safe 사용
        - `put()`메서드에 Synchronized 키워드를 사용합니다.
    - key에 null값 불가능
    - 보조해시를 사용하지 않기 때문에 충돌 발생 가능성이 더 높음.

<br />

#### Thread-safe가 무엇인가요?
두 개 이상의 Thread가 같은 자원(임계영역)에 접근해도 연산결과의 정합성에 문제 없이 안전을 보장할 수 있다는 의미입니다.

<br />

#### 버킷 동적 확장이 무엇인가요?
해시테이블은 내부적으로 배열을 사용하고 초기 기본 값이 16입니다. 따라서 배열이 다 차면 새로운 배열을 만들어야 하는데, 해시 테이블은 전체 크기의 3/4인 특정 임계값에 도달하면 크기를 2배씩 증가시킵니다. 이러다 보면 버킷의 개수가 2의 제곱형태가 되는데, 인덱스 값을 계산하게 되면 객체 해시값의 하위 비트만 사용하게 되어 해시 충돌이 쉽게 발생하는 문제점이 있습니다. 이를 해결하기 위한 개념이 **보조 해시 함수**입니다.

<br />

#### 보조 해시 함수가 무엇인데요?
객체의 해시값을 비트연산자로 조작하여 인덱스 값 분포를 고르게 하는 역할을 합니다. Java 8의 HashMap 보조 해시 함수는 상위 16비트 값을 xor 연산하는 형태입니다.

***

## Operating System
### Process를 설명해주세요.
프로세스란, 실행 중인 프로그램을 의미합니다. 즉, 실행파일 형태로 존재하던 프로그램이 Memory에 적재되어 CPU에 의해 실행(연산)되는 것을 프로세스라 합니다.
- Memory : CPU가 직접 접근할 수 있는 컴퓨터 내부의 기억장치입니다. 프로그램이 CPU에서 실행 되려면, 해당 내용이 Memory에 적재된 상태여야만 합니다.
    <p align="left"><img src="images/memory.png" width="50%"></p>



- CPU의 연산과 PC register
프로그램의 코드를 토대로 CPU가 실제 연산을 해야만 프로그램이 실행된다고 볼 수 있으며, 어떤 코드를 읽어야 하는가를 정하는 것은 CPU 내부에 있는 **PC(Program Counter) register**에 저장되어 있습니다. PC register에는 다음에 실행될 코드(명령어, instruction)의 주소값이 저장되어 있습니다. 즉, Memory에 적재되어있는 프로세스 Code 영역의 명령어중 다음 연산에서 읽어야할 명령어의 주소값을 PC register가 순차적으로 가리키게 되고, 해당 명령어를 읽음으로써 CPU가 연산을 하게 되면, process가 실행되는 것입니다.

<br />

#### Process의 Memory 영역에 대해서 설명해주세요.
프로세스가 운영체제에서 할당받는 메모리 공간은 Code, Data, Heap, Stack 영역으로 구분됩니다.
|영역|설명|
|:---|:---|
|Code|실행한 프로그램의 코드가 저장되는 메모리 영역|
|Data|프로그램의 전역 변수와 static 변수가 저장되는 메모리 영역|
|Heap|프로그래머가 직접 공간을 할당(malloc)/해제(free)하는 메모리 영역|
|Stack|함수 호출 시 생성되는 지역 변수와 매개 변수가 저장 되는 임시 메모리 영역|


***

### Multi Process에 대해서 설명해주세요.
2개 이상의 프로세스가 동시에 실행되는 것을 말합니다. 여기서 동시라는 표현은 동시성인 Concurrency와 병렬성인 Parallelism, 두 가지를 의미합니다.

동시성은 CPU core가 1개일 때, 여러 process를 짧은 시간 동안 번갈아 가면서 연산을 하게 되는 **시분할 시스템(Time Sharing Syste)** 으로 실행되는 것입니다.

병렬성은 CPU core가 여러개일 때, core들이 각각의 process를 연산함으로써 process가 동시에 실행되는 것입니다.

|동시성|병렬성|
|:---|:---|
|Single core|Multi core|
|동시에 실행되는 것 같아 보입니다.|실제로 동시에 여러 작업이 처리 됩니다.|

- 메모리관리 : Multi Process는 2개 이상의 process가 동시에 실행되며, 이 떄 process들은 CPU와 메모리를 공유하게 됩니다.