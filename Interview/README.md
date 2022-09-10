<p align="center" style="font-size:50px">
    <a href="https://github.com/lsw6684/ComputerScience">HOME</a>
</p>

___

<br />

# Interview
- [Data Structure](#data-structure)

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

#### 미리 예상한 것보다 더 많은 수의 data를 저장하느라 Array의 size를 넘어서게 됐습니다. 이 때, 어떻게 해겨할 수 있을까요?
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
Heap은 그 자체로 우선순위큐 구현과 일치합니다. 와전이진트리 구조로 Max Heap과 Min Heap으로 구분됩니다. Max힙을 예로 들자면, 각 child node의 값은 parent node보다 작아야 하며 root node에 저장된 값이 가장 큰 값이 됩니다.  

***

### Stack은 어떤 자료구조인가요? 
후입선출 LIFO(Last In First Out)의 자료구조입니다. push, pop 모두 O(1)이며 후위 표기법 연산, 괄호 유효성 검사, 웹 브라우저 방문기록(뒤로 가기), DFS 등이 있습니다.

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

<br />

#### Hash table에서 발생하는 Collision은 무엇이고 어떻게 해결할 수 있나요?
key의 해시값이 중복되는 경우를 말합니다. key가 다르더라도 해시값이 같을 수 있는데 이러한 collision이 적게 발생하고 연산속도가 빨라야 **좋은 hash function**이라고 할 수 있으며, 어쩔 수 없이 Collision이 발생한 경우 separate chaining이나 open addressing 등의 방식을 사용하여 해결합니다.
- separate chaining : Linked List를 사용하여 Collision 발생 시 노드(slot)를 추가하여 데이터를 저장합니다. 최악의 경우 O(n)이 발생할  수 있습니다.
- open addressing : Collision 발생 시 특정 규칙에 따라 hash table의 비어있는 slot을 찾습니다. 추가적인 메모리를 사용하지 않으므로, Linked List나 tree 자료구조를 사용하는 separate chaining방식에 비해 메모리를 적게 사용합니다. open addressing 방식은 찾는 방법에 따라 크게 Linear Probing, Quadratic Probing, Double Hashing으로 나뉩니다.
    - Linear Probing(선형 조사법) & Quadratic Probing(이차 조사법) : 선형 조사법은 충돌이 발생한 해시값으로 부터 일정 값만큼 건너 뛰어 빈 slot에 데이터를 저장하며 이차 조사법은 제곱수로 건너 뛰어 빈 slot을 찾아 데이터를 저장합니다.
        - 충돌 횟수가 많아지면 특정 영역에 데이터가 집중적으로 몰리는 클러스터링 현상이 발생하여 평균 탐색 시간이 증가하게 된다는 단점이 있습니다.
    - Double Hashing(이중해시, 중복해시) : Collision 시 open addressing 해결 방식 중 하나로, 클러스터링 문제가 발생하지 않도록 합니다. 최초의 해시값을 얻고 충돌 발생 시 또 다른 해시 함수를 이용합니다.

***
