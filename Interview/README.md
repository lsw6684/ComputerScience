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

<br />

#### Process의 Context가 무엇인가요?
process가 현재 어떤 상태로 수행되고 있는지에 대한 정보입니다. 해당 정보는 PCB에 저장합니다.

시분할 시스템에서는 한 process가 매우 짧은 시간동안 CPU를 점유하여 일정부분의 명령을 수행하고, 다른 process에게 넘깁니다. 그 후 차례가 되면 다시 CPU를 점유하여 명령을 수행합니다. 따라서 이전에 어디까지 명령을 수행했고, register에는 어떤 값이 저장되어 있었는지에 대한 정보가 바로 **context**입니다. context 정보들은 PCB(Process Control Block)에 저장합니다.

#### PCB에 저장되는 것들은 무엇이 있나요?
PCB는 운영체제가 process에 대해 필요한 정보를 모아놓은 자료구조입니다. 일반적으로 
- Process number
- Process state
- Program Counter(PC), 레지스터
- CPU 스케쥴링 정보, 우선순위
- 메모리 정보(해당 process의 주소 공간 등) 

PCB(Process Control Bolck) : OS가 프로세스를 표현한 자료구조입니다. PCB에는 프로세스의 중요한 정보가 포함되어 있기 때문에, 일반 사용자가 접근하지 못하도록 보호된 메모리 영역 안에 저장됩니다. 일부 OS에서 PCB는 커널 스택에 위치합니다. 이 메모리 영역은 보호를 받으면서도 비교적 접근하기가 편리하기 때문입니다.
|PCB||
|:---|:---|
|Process State|new, running, waiting, halted 등의 state가 있습니다.|
|Process Number|해당 process의 number|
|Program Counter(PC)|해당 process가 다음에 실행할 명령어의 주소를 가리킵니다.|
|Registers|컴퓨터 구조에 따라 다양한 수와 유형을 가진 register값들을 가집니다.|
|Memory limits|base register, limit register, page table, sgment table 등|

<br />

#### Context switch에 대해서 설명해주세요.
한 process에서 다른 process로 CPU제어권을 넘겨주는 것을 말합니다. 이 때 이전의 프로세스 상태를 **PCB에 저장하여 보관**하고 새로운 프로세스의 **PCB를 읽어서 보관된 상태를 복구**하는 작업이 이루어집니다.

<br />

#### process의 state에는 어떤 것들이 있나요?
process는 실행(running), 준비(ready), 봉쇄(wait, sleep, blocked) 세 가지 상태로 구분됩니다.
- 실행 : 프로세스가 CPU를 점유하고 명령을 수행중인 상태
- 준비 : CPU만 할당받으면 즉시 명령을 수행할 수 있도록 준비된 상태
- 봉쇄 : CPU를 할당받아도 명령을 실행할 수 없는 상태 - `I/O작업 대기`

***

### Multi Process에 대해서 설명해주세요.
2개 이상의 프로세스가 동시에 실행되는 것을 말합니다. 여기서 동시라는 표현은 동시성인 Concurrency와 병렬성인 Parallelism, 두 가지를 의미합니다.

동시성은 CPU core가 1개일 때, 여러 process를 짧은 시간 동안 번갈아 가면서 연산을 하게 되는 **시분할 시스템(Time Sharing Syste)** 으로 실행되는 것입니다.

병렬성은 CPU core가 여러개일 때, core들이 각각의 process를 연산함으로써 process가 동시에 실행되는 것입니다.

|동시성|병렬성|
|:---|:---|
|Single core|Multi core|
|동시에 실행되는 것 같아 보입니다.|실제로 동시에 여러 작업이 처리 됩니다.|

- 메모리관리 : Multi Process는 2개 이상의 process가 동시에 실행되며, 이 떄 process들은 CPU와 메모리를 공유합니다. 여기서 서로 다른 process의 영역을 침범하지 않고 자신의 memory영역에만 접근하도록 OS가 관리해줍니다.

***

### Thread가 무엇인가요?
한 process 내에서 실행되는 동작(기능 function)의 단위입니다. 각 Thread는 속해있는 process의 Stack 메모리를 제외한 나머지 Memory 영역인 Code, Data, Heap을 공유할 수 있습니다.

Thread는 process 내에서 독립적인 기능을 수행합니다. 독립적인 기능을 수행한다는 것은 독립적으로 함수를 호출함을 의미합니다.

<br />

#### Thread는 왜 독립적인 Stack Memory 영역이 필요한가요?
Stack 영역은 함수 호출 시 전달되는 인자, 함수의 Return Address, 함수 내 지역변수 등이 저장되며 각 thred가 함수 호출 시 각각의 Stack memory를 사용합니다.


<br />

#### Multi thread는 무엇인가요?
하나의 process가 동시에 여러개의 일을 수행할 수 있도록 해주는 것입니다. 즉, 하나의 process(실행된 하나의 program)에서 여러 작업을 병렬로 처리하기 위한 단위입니다.

<br />

#### process와 thread를 비교하여 설명해주세요.
process는 운영체제로부터 자원을 할당받는 작업의 단위이고, thread는 process가 할당받은 자원을 이용하는 실행의 단위입니다. 즉, process는 실행파일이 memory에 적재되어 CPU를 할당받아 실행되는 것입니다. 

Thread는 한 process 내에서 실행되는 동작의 단위이며, stack 영역을 제외한 code, data, heap 영역을 공유합니다.

<br />

#### Multi process와 Multi thread를 비교하여 설명해주세요.
- Multi thread는 Multi process보다 적은 메모리 공간을 차지하고, **Context Switching**이 빠릅니다.
- Multi process는 Multi thread보다 많은 메모리공간과 CPU 시간을 차지합니다.
- Multi thread는 동기화 문제와 하나의 thread 장애로 전체 thread가 종료될 위험이 있습니다.
- Multi process는 하나의 process에 문제가 발생해도 다른 process에 영향을 주지 않아, 안정성이 높습니다.
- 메모리 구분이 필요한 경우 Multi process가 유리합니다.
- Context Switching이 자주 일어나고, 데이터 공유가 빈번한 경우, 그리고 자원을 효율적으로 사용해야 되는 경우 Multi thread가 유리합니다.

    ||Multi Process|Multi Thread|
    |:---|:---|:---|
    |메모리 사용<br />CPU 시간|많음|적음|
    |Context<br />Switching|느림|빠름|
    |안전성|높음|낮음|

<br />

#### Multi thread가 Multi process보다 좋은 점은 무엇인가요?
Multi process를 이용하던 작업을 Multi thread로 구현할 경우, 메모리 공간과 시스템 자원 소모가 줄어들게 됩니다. 또한 process를 생성하고 자원을 할당하는 등의 system call을 생략할 수 있기 때문에, 자원을 효율적으로 관리할 수 있습니다. 뿐만 아니라 Context swtiching 시 캐시 메모리를 초기화할 필요가 없어서 속도가 빠릅니다.

데이터를 주고 받을 때를 비교해 보면, process 간의 통신(IPC)보다 Multi thread 간의 통신 비용이 적기 때문에, 오버헤드가 적습니다.
- IPC(Inter-Process Communication) : process는 각각의 독립적 주소를 가지는데, 다른 process가 이 주소공간을 참조하는 것은 허용하지 않습니다. 그렇기 때문에 다른 process와 데이터를 주고받을 수 없습니다. 이를 해결하고자 운영체제는 IPC기법을 통해 process들 간에 통신을 가능하게 합니다.<br />
process간 통신(IPC)에는 기본적으로 공유메모리(shared memory)와 메시지 전달(message passing)의 두 가지 모델이 있습니다.
    - **공유 메모리(shared memory)** : process들이 주소 공간의 일부를 공유합니다. 공유한 메모리 영역에 읽기/쓰기를 통해서 통신을 수행합니다. process가 공유 메모리할당을 kernel에 요청하면, kernel은 해당 process에 메모리 공간을 할당해줍니다. 공유 메모리 영역이 구축된 이후에는 모든 접근이 일반적인 메모리 접근으로 취급되기 때문에 더 이상 kernel의 도움 없이도 각 process들이 메모리 영역에 접근할 수 있습니다. 따라서 kernel의 관여 없이 데이터 통신을 할 수 있기 때문에, **IPC속도가 빠르다**는 장점이 있습니다. <br />
    공유 메모리 방식은 process 간의 통신을 수월하게 만들지만, 동시에 같은 메모리 위치에 접근하게 되면 일관성 문제가 발생할 수 있습니다. 이에 대해서는 kernel이 관여하지 않기 때문에 process들 끼리 직접 공유 메모리 접근에 대한 동기화 문제를 책임져야 합니다.
    - **메시지 전달(message passing)** : 통상 system call을 사용하여 구현됩니다. kernel을 통해 send(message)와 receive(message)라는 두 가지 연산을 제공받습니다. 예를 들면, process1이 kernel로 message를 보내면, kernel이 process2에게 message를 보내주는 방식으로 작동합니다.<br />
    메모리 공유보다는 속도가 느리지만, **충동을 회피할 필요가 없기**때문에 적은 양의 데이터를 교환하는 데 유용합니다. 또, 구현하기 쉽다는 장점이 있습니다. `pipe, socket, message queue`

<br />

#### IPC의 예시를 들어주실 수 있나요?
IPC는 크게 공유 메모리 모델과 메시지 전달 모델로 나눌 수 있습니다. 공유 메모리 모델은 주소 공간의 일부를 공유하며 공유한 메모리 영역에 read/write를 통해 통신하게 되는데, 예시로는 공유메모리와 POSIX가 있습니다. 메시지 전송 모델의 경우, kernel을 통해 send/receive 연산으로 데이터를 전송합니다. 예시로는 `pipe, socket, message queue`등이 있습니다.

<br />

#### Multi process환경에서 process 간에 데이터를 어떻게 주고 받을까요?
원칙적으로 process는 독립적 주소 공간을 가지며, 다른 process의 주소 공간을 참조할 수 없습니다. 하지만, 경우에 따라 운영체제는 process 간의 자원 접근을 위한 매커니즘인 **프로세스 간 통신(IPC)**을 제공합니다. `pipe, socket, 공유 메모리`

<br />

#### Multi thread가 Multi process보다 안 좋은 점은 무엇인가요?
thread 간의 자원 공유 시 동기화문제가 발생할 수 있어서, 프로그램 설계 시 주의가 필요하고, 하나의 thread에 문제가 생기면, process 내의 다른 thread에도 문제가 생길 수 있습니다.

<br />

#### 공유 메모리와 메시지 전달 모델의 장단점을 설명해주세요.
공유 메모리 모델은 초기 공유 메모리 할당을 제외하면, kernel 관여 없이 통신을 유지할 수 있기 때문에 빠른 속도를 자랑합니다. 하지만, process가 동시에 메모리에 접근하기 때문에, 동기화 과정을 구현해야 한다는 단점이 있습니다.

메시지 전달 모델은 kernel을 통해 데이터를 주고 받기 때문에, 통신 속도가 느리다는 단점이 있습니다. 하지만, kernel의 제어로 동기화 문제를 신경쓰지 않아도 됩니다.

***

### Multi process/thread 환경에서 동기화 문제를 어떻게 해결하나요?
Mutex와 Semaphore 기법 등을 사용할 수 있습니다. 
- Mutex란 1개의 스레드만이 공유 자원에 접근할 수 있도록 하여, 경쟁 상황(race condition)을 방지하는 기법입니다. 공유 자원을 점유하는 thread가 `lock`을 걸면, thread는 `unlock` 상태가 될 때까지 해당 자원에 접근할 수 없습니다.
    ```c++
    acquire() // entry sction

    // critical section

    release() // exit section
    ```
- Semaphore란 S개(세마포 변수의 값만큼)의 thread만이 공유 자원에 접근할 수 있도록 제어하는 동기화 기법입니다. Semaphore 기법에서는 정수형 변수 `S(세마포)` 값을 가용한 자원의 수로 초기화하고, 자원에 접근할 때는 `S--` 연산을 수행하여 세마포 값을 감소시키고 자원을 방출할 때는 `S++`연산을 수행하여 세마포 값을 증가시킵니다. 이 때 세마포 값이 0이 되면 모든 자원이 사용 중임을 의미하고, 이후 자원을 사용하려는 프로세스는 세마포 값이 0보다 커질 때까지 `block`됩니다.
    ```c++
    wait(S) // entry section

    // critical section

    signal(S) // exit section
    ```
    - Binary Semaphore : Semaphore 값이 0, 1만 가질 수 있는 경우로, Mutex랑 유사하게 작동합니다.
- Busy waiting은 자원을 얻기 위해 권한을 얻을 때까지 확인하는 것을 의미합니다. CPU의 자원을 쓸데 없이 낭비하기 때문에 권장되지 않는 동기화 방식입니다.

<br />

#### 임계영역(critical section)에 대해 설명해주세요.
둘 이상의 process/thread가 동시에 동일한 자원에 접근하도록 하는 프로그램 코드 부분을 의미합니다. 중요한 특징중 하나는, 한 process/thread가 자신의 임계구역에서 수행하는 동안에는 다른 process/thread들은 그들의 임계구역에 들어갈 수 없어야 한다는 사실입니다. 즉, 임계영역 내의 코드는 원자적으로(atomically) 실행이 되어야 합니다.

원자적으로 실행되기 위해서 각각의 process/thread는 자신의 임계구역으로 진입하려면 진입 허가를 요청해야합니다. 이 부분을 entry section이라고 하고, 진입이 허가되면 임계영역을 실행할 수 있습니다. 임계영역이 끝나고 나면 exit section으로 퇴출을 하게 됩니다. 이렇게 임계영역의 원자성을 보장하는 것을 동기화라고 하며, 대표적으로 `Mutext`와 `Semaphore`가 있습니다.

***
### 

***