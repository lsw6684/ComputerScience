<p align="center" style="font-size:50px">
    <a href="https://github.com/lsw6684/ComputerScience">HOME</a>
</p>

***

<br />

# Data Structure
- [자료구조](#자료구조)
- [배열](#배열)
- [연결 리스트](#연결-리스트)
- [Stack and Queue](#stack-and-queue)
- [Tree](#tree)
- [Binary Tree](#binary-tree)
- [Binary Search Tree](#binariy-search-tree)

## 자료구조
좋은 알고리즘의 기반이 되며 속도, 메모리 등을 효율적으로 관리할 수 있게 하는 방법론을 제시합니다.

## 배열
논리적, 물리적 순서가 일치하는 선형 자료구조로 일정 크기의 메모리를 할당받아 사용합니다.
- 장점 : 인덱스를 사용하여 `Big-O(1)`로 접근 가능합니다.
- 단점 : 삽입, 삭제 등에 대한 Cost가 높습니다. `Big-O(1)` 수행과 `shift`로 후의 원소들을 이동시켜야 하는 작업이 요구됩니다. `Time complexity : Worst Case = O(n)`

## 연결 리스트
선형 자료구조로 물리적 위치와 논리적 위치가 다를 수 있으며, 각 원소는 자신 다음 원소의 물리적 위치를 가집니다. 자료가 추가될 때마다 메모리를 할당받습니다.
- 장점 : `shift`필요 없이, 삭제/삽입를 수행하여 상대적으로 효율적입니다.
- 단점 : 논리적 위치는 순서대로 되어있으나 물리적으론 순서대로 되어있지 않기 때문에 원하는 index에 접근하려면 0번 index부터 차례로 접근합니다.

## Stack and Queue
### Stack
선형 자료구조로 Last In First Out. 
### Queue
선형 자료구조로 First In First Out.

## Tree
스택, 큐와 같이 선형 구조가 아닌 비선형 자료구조로 계층적 관계를 표현합니다.
### 트리의 구성요소
- Node(노드) : 트리를 구성하는 각각의 요소를 의미합니다.
- Edge(간선) : 노드와 노들를 연결합니다.
- Root Node(루트 노드) : 최상위 노드입니다.
- Terminal Node(=Leaf Node, 단말 노드) : 하위 노드를 가지지 않는 마지막 노드입니다.
- Internal(내부 노드, 비단말 노드) : 단말 노드를 제외한 모든 노드입니다. `루트 포함`
- 특정 노드의 차수 : 서브트리의 수(branch)를 의미하며 단말노드는 차수가 0입니다.
- 트리의 차수 : 트리가 보유한 노드들의 최대 차수를 의미합니다.
- 레벨 : 루트가 레벨1이며 하위 노드의 레벨은 상위 노드의 레벨 + 1 입니다.

## Binary Tree
루트 노드를 중심으로 두 개의 서브 트리로 나뉘며, 나뉘어진 트리 또한 재귀적으로 나뉩니다.
- 포화 이진 트리 : 모든 레벨이 가득 찬 이진 트리.
- 완전 이진 트리 : 위에서 아래로, 왼쪽에서 오른쪽으로 모두 채워진 이진 트리.
- 정 이진 트리 : 모든 노드가 0개 혹은 2개의 자식 노드만을 갖는 이진 트리.

## Binary Search Tree
BST, 이진 트리이며, 위치를 찾기에 효율적인 규칙으로 데이터를 저장합니다.
### BST 규칙
1. 이진 탐색 트리의 노드에 저장된 키는 유일합니다.
2. 부모의 키가 왼쪽 자식 노드의 키보다 큽니다.
3. 부모의 키가 오른쪽 자식 노드의 키보다 작습니다.
4. 모든 서브트리도 이진 탐색 트리입니다. 