<p align="center" style="font-size:50px">
    <a href="https://github.com/lsw6684/ComputerScience">HOME</a>
</p>

***

<br />

# ALGORITHM (Including Data Structure)
- [CPP 입출력 속도 향상](#cpp-입출력-속도-향상)
- [시간복잡도 & 공간복잡도](#시간복잡도--공간복잡도)
- [배열](#배열)
- [벡터](#벡터)
- [연결 리스트](#연결-리스트)
- [스택, 큐, 덱](#스택-큐-덱)
- [BFS](#bfs)
- [DFS](#dfs)
- [재귀](#재귀)
- [백트래킹](#백트래킹)
- [시뮬레이션](#시뮬레이션)
- [정렬](#정렬)
- [Greedy](#greedy)
- [Dynamic Programming](#dynamic-programming)

<br />

## CPP 입출력 속도 향상
- std::endl → **"\n"** : endl은 버퍼를 비우고 출력을 진행하기 때문에 상당한 시간을 요구합니다. \n을 사용하는 것이 **월등히 빠르다**고 할 수 있습니다.

    `#define endl "\n"`을 상단에 정의하면 \n을 endl로도 표현할 수 있습니다. (전역변수 std 사용 시 주의❗)
- ios::sync_with_stdio(0), cin.tie(0) - 메인함수 안에 선언
    - ios::sync_with_stdio(0) : cin과 cout은 stream상에서 분리되어 있기 때문에 동기화할 시간이 필요합니다. 그렇기 때문에 앞에서 언급된 문장을 선언함으로써 동기화를 끊어야 합니다. (해당 방법을 사용할 시 scanf/printf를 사용하면 안 됩니다❗)
    - cin.tie(0) : cin은 endl과 같은 개념으로 버퍼를 사용하기 때문에 속도가 느립니다. 이러한 과정을 생략하기 위해 사용됩니다.
- using namespace std - 전역 : 많은 사람들이 전역변수를 사용하는 것은 프로그래밍 관점으로 봤을 때 충돌을 야기할 수 있으며 지양해야 하는 부분이라고 말합니다. 저 또한 그렇게 생각합니다. 하지만, 코딩 테스트를 위한 코딩은, 남에게 보여주거나 유지보수를 고려해야 하는 클린 코딩이 중요한 것이 아니라 **속도와 순간의 편리성을 우선**으로 해야 한다고 생각합니다.

<br />

## 시간복잡도 & 공간복잡도
- **시간복잡도(Time Complexity) :** 입력의 크기와 문제를 해결하는데 걸리는 시간의 상관관계
  - 빅오표기법 (Big-O Notation) : 주어진 식을 값이 가장 큰 대표항만 남겨서 나타내는 방법
    - O(N) : 5N + 3, 2N + 10lgN, 10Nfil
    - O(N²) : N² + 2N + 4, 6N² + 20N, 10lgN
    - O(NlgN) : NlgN + 30N + 10, 5NlgN + 6
    - O(1) : 5, 16, 36
<p align="center"><img src="images/timeComplexity.png" width="50%"></p>

<p align="center"><img src="images/bigO.png" width="50%"></p>

**ex 1) O(N)**
```cpp
int func(int arr[], int n) {
    int cnt = 0;                    // cnt 1번
    for(int i = 0; i < n; i++)      // for( 1번; n번; n번 )
        if(arr[i] % 5 == 0) cnt++;  // if(1번, 1번) 1번
    }
    return cnt;                     // 1 + 1 + n(2 + 2 + 1) + 1 = 5n + 3                                   
}   
```
n이 100만이면 약 500만의 연산이 필요하여 1초 안에 **가능**.

n이 10억이면 약 50억번의 연사이 필요하여 1초 안에 **불가능**.

※ **5n+3 → n에 비례** 한다고 표현합니다.

<br />

**ex 2) O($\sqrt{N}$)**

```cpp
int func(int N) {
    for(int i = 1; i * i <= N; i++) {
        if(i*i == N) return 1;
    }
    return 0;
}
```

</br>

**ex 3) O(lgN) - N이 2<sup>k</sup> 이상 2<sup>k+1</sup> 미만일 때 O(k)**

```cpp
int func(int N) {
    int val = 1;
    while(2*val <= N) val *=2;
    return val;
}
```

</br>

**ex 4) Confusing❗**
```cpp
// O(N) 벡터도 메인함수에서 복사본을 보내는 것입니다. 
// N개의 복사본을 보내기 때문에 O(N). 원본도 변하지 않습니다.
bool cmp1 (vector<int> v1, vector<int> v2, int idx) 
    return v1[idx] > v2[idx];

// O(1) 참조자를 사용하여 참조 대상의 주소 정보만 넘어가기 때문에 O(1).
// 원본도 바뀝니다.
bool cmp2 (vector<int>& v1, vector<int>& v2, int idx)
    return v1[idx] > v2[idx];
```

<br />

- **공간복잡도(Time Complexity) :** 입력의 크기와 문제를 해결하는데 필요한 공간의 상관관계
    - 메모리 제한이 `512MB`인 경우 `1.2억개의 int` 선언 가능 

<br />

## 배열
- 메모리 상에 원소를 **연속**하게 배치한 자료구조입니다.
- 배열의 끝에 원소를 추가/제거/확인/변경 하는 경우 **O(1)**. k번째 원소를 확인, 변경 가능.
- 임의의 위치에 원소를 추가/제거 하는 경우 **O(N)**.
- 추가적으로 소모되는 메모리의 양(**=overhead**)가 거의 없습니다.
- [**Cache hit rate**](#cache-hit-ratio)가 높습니다.
- 메모리 상에 연속한 구간을 잡아야 해서 할당에 제약이 걸립니다.
- 선형 자료구조입니다.
    - ### **Cache hit ratio**
    ```
    Cache Hit : User process가 요구하는 데이터기 있을 경우
    Cache Miss : User Process가 요구하는 데이터가 없을 경우
    Chache hit ratio는 Buffer Cache에서 바로 읽혀진 비율로 캐쉬의 적중률이라고 할 수 있습니다.
    ```
- fill함수 활용 권장
    ```cpp
    int a[21];
    fill(a, a+3, 0);                    // a의 0번째부터 세 번째 까지 0으로 채웁니다.
    
    int b[10][10];
    fill(b[0], b[0]+5, 1);              // b의 1행의 첫 번째부터 다섯 번째까지 1로 채웁니다.
    ```
- 🎁 O(N<sup>2</sup>)이 아닌 O(N) 비교
    - Q) 임의의 자연수 N개로 이루어진 배열에서 합이 100인 서로 다른 위치의 두 원소가 존재하면 1, 그렇지 않으면 0을 반환하는 함수.
        ```cpp
        이중 for문(O(N<sup>2</sup>))으로 비교하는 것이 아닌 한 개의 for문(O(N))으로도 가능합니다.
        int func(int arr[], int N) {
            int occur[101] = {};
            for(int i = 0 ; i < N; i++) {
                if(occur[100-arr[i]])           // 값이 1(합 100)이면 참
                    return 1;
                occur[arr[i]] = 1;
            }
            return 0;
        }
        ```

<br />

## 벡터
- 원소가 메모리에 연속하여 저장되어 있기 때문에 O(1)에 인덱스로 접근 가능.
- loop comparison
    ```cpp
    vector<int> v1 = {1, 2, 3, 4, 5, 6};

    // 1. range-based for loop (since c++11)
    for(int e : v1)
        cout << e << ' ';               // e를 수정하면 원본 v1도 바뀝니다.
    
    // 2. usual
    for(int i = 0; i < v1.size(); i++)
        cout << v1[i] << ' ';

    size는 정수가 아닌 unsigned int를 반환합니다.
    // 3. ***wrong***
    for(int i = 0 ; i <= v1.size() - 1; i++)
        cout << v[i] << ' ';
    ```

<br />

## 연결 리스트
- 원소를 저장할 때 그 다음 원소가 있는 위치를 포함시키는 방식으로 저장하는 자료구조입니다.
- 선형 자료구조입니다.
<p align="center"><img src="images/linkedList.png" width="80%"></p>

　　　　　　**특정 원소릴 알면 후의 원소들도 알 수 있습니다.**
- k 번째 원소를 확인/변경하기 위해 **O(k)** 가 필요합니다.
- 임의의 위치에 원소를 추가/제거 하기 위해 **O(1)** 이 필요합니다.(*단, 위치를 알고 있는 경우*)
- 원소들이 메모리 상에 연속해있지 않아 [**Cache hit rate**](#cache-hit-ratio)가 낮지만 할당이 다소 쉽습니다.
    - 단일 연결 리스트(Singly Linked List) : 각 원소가 자신의 다음 원소의 주소를 포함합니다.
    - 이중 연결 리스트(Doubly Linked List) : 이전 원소와 다음 원소의 주소를 포함합니다. 원소를 하나 더 가지기 때문에 메모리를 더 사용합니다.
    - 원형 연결 리스트(Circular Linked Likst) : 단일 혹은 이중 연결 리스트 상태에서 끝이 처음과 연결되어있습니다.
- 임의의 원소에 대한 작업이 필요한 경우 용이합니다.
- 🎁 배열 vs 연결리스트

<p align="center"><img src="images/arrayVSlinkedlist.png" width="80%"></p>

- 야매 연결 리스트 (실무❌, STL 사용 불가한 코딩 테스트⭕)
    ```cpp
    const int MX = 1000005;         
    int dat[MX], pre[MX], nxt[MX];                      // dat - i번째 원소의 값
    int unused = 1;                                     // pre - 이전, nxt - 다음 원소의 값
    // 0은 시작점을 나타내기 위한 dummy node.   unused부터 새로운 원소가 들어갈 수 있고 1씩 증가.
    fill(pre, pre+MX, -1);                              // -1 : 이전(pre) 혹은 다음(nxt) 원소가 존재하지 않음.
    fill(nxt, nxt+MX, -1);                  
    ```
-   ```cpp
    #include<iostream>
    #include<list>
    #define endl "\n"
    using namespace std;

    int main() {
        ios::sync_with_stdio(0), cin.tie(0);
        list<int> L = { 1,2 };	                    // 1 2
        list<int>::iterator t = L.begin();	            // c++11 이상부터 auto t = L.begin() 가능
        L.push_front(10);		                    // 10 1 2
        cout << *t << endl;		                    // t가 가리키는 값 = 1 출력
        L.push_back(5);			            // 10 1 2 5
        L.insert(t, 6);			            // t가 가리키는 곳 앞에 6을 삽입, 10 6 1 2 5
        t++;					    // t를 1칸 앞으로 전진? t가 가리키는 값은 2.
        t = L.erase(t);			            // t가 가리키는 값 제거. 10 6 1 5, 이제 t는 5를 가리킴

        cout << *t << endl;	                            // 5
        
        for (auto i : L) cout << i << ' ';	// c++11 이상부터 가능. 불가능 하면 아래 방법.
        cout << endl;
        for (list<int>::iterator it = L.begin(); it != L.end(); it++)
            cout << *it << ' ';
    }
    ```
- 🎁 원형 연결 리스트 내의 임의의 노드 하나가 주어졌을 때 해당 List의 길이를 효율적으로 구하는 방법은?
    ```cpp
     시작점을 저장하고 동일한 노드가 나올 때 까지 다음 노드로 이동하면 됩니다.
    공간복잡도 O(1), 시간복잡도 O(N)의 효율을 갖습니다.
    ```
- 🎁 중간에서 만나는 두 연결 리스트의 시작점들이 주어졌을 때 만나는 지점을 구하는 방법은?

<p align="center"><img src="images/meetingPoint.png" width="80%"></p>
 
```cpp
1. 두 시작점 각각에 대해 끝까지 진행시키고 각각의 길이를 구합니다.
2. 그 후 다시 시작점으로 돌아와서 더 긴쪽을 둘의 차이만큼 앞으로 먼저 이동시킵니다.
3. 두 점을 동시에 한 칸씩 전진시키다 보면 동일한 점에서 만납니다.
   🙂 공간복잡도 O(1), 시간복잡도 O(A+B)로 구할 수 있습니다.
```
- 🎁 주어진 연결 리스트 안에 사이클이 있는지 판단하라.

<p align="center"><img src="images/floyd.png" width="70%"></p>

```cpp
Floyd's cycle-finding algorithm을 이용하여, 공간복잡도 O(1), 시간복잡도 O(N)으로 구할 수 있습니다.
한 칸씩 가는 커서와 두 칸씩 가는 커서를 동일 시점에서 출발 시키면, 사이클이 있을 경우 두 커서는 만나게 됩니다.
반대로 사이클이 존재하지 않다면, 만나지 못하고 연결 리스트의 끝에 도달하게 됩니다.
```

<br />

## 스택, 큐, 덱
상위 세 가지 자료구조는 원소를 삽입하고 제거하는 위치가 정해져 있어서 **Restricted Structured**로 불리기도 합니다.
- 스택
    - FILO - First In Last Out
    - 한쪽 끝에서만 원소를 넣고 뺄 수 있습니다.
    - 원소의 추가, 제거, 그리고 상단의 원소 확인이 O(1)입니다.
    - 최상단의 원소를 제외한 원소는 확인/변경이 **원칙적으로는 불가능**합니다.
- 큐
    - FIFO - First In First Out
    - 한쪽 끝에서 원소를 넣고 반대쪽 끝에서 원소를 뺄 수 있는 자료구조입니다.
    - 원소의 추가, 제거, 그리고 앞/뒤 원소들의 확인이 O(1)입니다.
    - 맨 앞/뒤가 아닌 나머지 원소들의 확인/변경이 **원칙적으로는 불가능**합니다.
    -큐가 비어있을 때 호출하면 런타임에러가 발생할 수 있습니다.
- 덱
    - deque, Double Ended Queue로 양쪽 끝에서 삽입, 삭제가 가능합니다.
    - 원소의 추가, 제거, 그리고 앞/뒤의 원소들의 확인이 O(1)입니다.
    - 맨 앞/뒤가 아닌 나머지 원소들의 확인/변경이 **원칙적으로는 불가능**합니다. ***STL deque에서는 인덱스로 접근 가능***합니다.

<br />

## BFS
- Breadth First Search, 다차원 배열에서 각 칸을 방문할 때 너비를 우선으로 방문하는 알고리즘입니다.
- 자료구조에서 정점과 간선으로 이루어진 그래프에서 모든 노드를 방문하기 위한 알고리즘입니다.
- 노드가 N개일 때 O(N). **행이 R이고 열이 C이면 O(RC)**
1. 시작 점을 Queue에 push하고 방문했다는 표시를 남깁니다.
2. Queue의 원소를 꺼내어 상하좌우 인접한 칸에 대해 3번을 진행합니다.
3. 방문하지 않은 인접 공간에 방문했다는 표시를 남기고 Queue에 push합니다.
4. Queue가 empty상태가 될 때까지 2번을 반복합니다.

- pair 활용 : 두 자료형을 묶어서 사용할 수 있습니다.
    ```cpp
    #include<iostream>
    using namespace std;
    int main() {
        pair<int, int> t1 = make_pair(10, 13);	                    // pair 생성
        pair<int, int> t2 = { 4, 6 };	                            // since c++11
        cout << t2.first << ' ' << t2.second << '\n';	            // 원소 접근
        if (t2 < t1) cout << "t2 < t1";                                 // first 비교하고 second 비교
    }    
    4 6
    t2 < t1
    ```
- BFS 구현
    ```cpp
    #include <iostream>
    #include <queue>
    using namespace std;
    #define endl '\n'
    #define X first
    #define Y second				                    // pair에서 first, second 줄여 쓰기 위함.
    int board[502][502] =
    {
        {1,1,1,0,1,0,0,0,0,0},
        {1,0,0,0,1,0,0,0,0,0},
        {1,1,1,0,1,0,0,0,0,0},
        {1,1,0,0,1,0,0,0,0,0},
        {0,1,0,0,0,0,0,0,0,0},
        {0,0,0,0,0,0,0,0,0,0},
        {0,0,0,0,0,0,0,0,0,0}
    };						                    // 1 == 방, 0 == 벽
    bool vis[502][502];						    // 해당 칸을 방문했는지 여부 저장
    int n = 7, m = 10;					            // 행, 열의 수
    int dx[4] = { 1, 0, -1, 0 };
    int dy[4] = { 0, 1, 0, -1 };				            // 상하좌우 네 방향 의미
    int main()
    {
        ios::sync_with_stdio, cin.tie(0);
        queue<pair<int, int>> Q;
        vis[0][0] = 1;					            // (0, 0) 시작, 방문
        Q.push({ 0,0 });						    // Q에 방문한 곳 push
        while (!Q.empty()) {                                            // Q가 empty가 될 때까지
            pair<int, int> cur = Q.front();
            Q.pop();
            cout << '(' << cur.X << ',' << cur.Y << ") -> ";
            for (int dir = 0; dir < 4; dir++) {	                    // 상하좌우 살피기
                int nx = cur.X + dx[dir];
                int ny = cur.Y + dy[dir];		                    // nx, ny에 dir에서 정한 방향의 인접한 칸의 좌표
                if (nx < 0 || nx >= n || ny < 0 || ny >= m) continue;   // 범위 밖 제외
                if (vis[nx][ny] || board[nx][ny] != 1) continue;	    // 이미 방문한 칸, 벽 제외
                vis[nx][ny] = 1;				            // (nx, ny) 방문
                Q.push({ nx,ny });
            }
        }
    }
    (0,0) -> (1,0) -> (0,1) -> (2,0) -> (0,2) -> (3,0) -> (2,1) -> (3,1) -> (2,2) -> (4,1) ->
    ```

<br />

## DFS
- Depth First Search, 다차원 배열에서 각 칸을 방문할 때 깊이를 우선으로 방문하는 알고리즘입니다.
- 모든 칸이 Stack에 1번씩 들어가므로 시간복잡도는 칸이 N개일 때 O(N)입니다.
- 거리 측정은 불가능합니다. (거리 측정은 [BFS사용](#bfs))
1. 시작하는 칸을 Stack에 넣고 방문 표시를 남깁니다.
2. Stack에서 원소를 꺼내고 해당 원소의 상하좌우로 인접한 칸에 대해 3번을 진행합니다.
3. 해당 칸을 이전에 방문했다면 아무 것도 하지 않고(Continue), 처음으로 방문했다면 방문했다는 표시를 남기며 해당 칸을 Stack에 삽입합니다.
4. Stack이 빌 때 까지 2번을 반복합니다.
- DFS 구현
    ```cpp
    #include <iostream>
    #include <stack>
    #define X first
    #define Y second
    using namespace std;

    int board[502][502] ={ 
    {1,1,1,0,1,0,0,0,0,0},
    {1,0,0,0,1,0,0,0,0,0},
    {1,1,1,0,1,0,0,0,0,0},
    {1,1,0,0,1,0,0,0,0,0},
    {0,1,0,0,0,0,0,0,0,0},
    {0,0,0,0,0,0,0,0,0,0},
    {0,0,0,0,0,0,0,0,0,0} };
    bool vis[502][502];
    int n = 7, m = 10;
    int dx[4] = { 1, 0, -1, 0 };
    int dy[4] = { 0, 1, 0, -1 };

    int main() {
        ios::sync_with_stdio(0), cin.tie(0);
        stack<pair<int, int>> S;
        vis[0][0] = 1;
        S.push({ 0, 0 });

        while (!S.empty()) {
            pair<int, int> cur = S.top(); S.pop();
            cout << '(' << cur.X << ',' << cur.Y << ") -> ";
            for (int dir = 0; dir < 4; dir++) {
                int nx = cur.X + dx[dir];
                int ny = cur.Y + dy[dir];
                if (nx < 0 || nx >= n || ny < 0 || ny >= m) continue;
                if (vis[nx][ny] || board[nx][ny] != 1) continue;
                vis[nx][ny] = 1;
                S.push({ nx, ny });
            }
        }
    }
    ```

<br />

## 재귀
하나의 함수에서 자기 자신을 다시 호출하여 작업을 수행하는 알고리즘입니다. <br />
- 특정 입력에 대하여 자기 자신을 호출하지 않고 종료되어야 하며 **(Base condition||Base case), 모든 입력은 base condition으로 수렴**해야 합니다.
- 모든 재귀 함수는 반복문으로 동일한 구현이 가능합니다.
- 재귀는 반복문에 비해 코드가 간결하지만, 메모리/시간 영역에서는 손해를 봅니다.
- 재귀함수는 자기 자신을 부를 때 **스택 영역에 계속 누적**됩니다.
- **BOJ 1629 - 곱셈 : mod 연산**

    ```cpp
    #include<iostream>
    #define ll long long
    using namespace std;

    ll mod(ll a, ll b, ll c)
    {
        ios::sync_with_stdio(0), cin.tie(0);
        if (b == 1) return a % c;
        ll val = mod(a, b / 2, c);
        val = val * val % c;
        if (b % 2 == 0) return val;
        return val * a % c;
    }

    int main() {
        int a, b, c;
        cin >> a >> b >> c;
        cout << mod(a, b, c);
    }
    ```

<br />

## 백트래킹
현재 상태에서 가능한 모든 후보군(선택지)을 따라 들어가며 탐색하는 알고리즘입니다. <br />
`프린세스 메이커, 역전 재판 등 선택지에 의해 결과가 달라지는 게임을 생각합니다. 전 미연시 안합니다. 예시로 찾아져서 쓴겁니다.`

<br />

## 시뮬레이션

<br />

## 정렬
### 기초 정렬 : O(N<sup>2</sup>)
<p align="center"><img src="images/정렬.png" width="50%"></p>

```cpp
int arr[10] = {3, 2, 7, 116, 62, 345, 1, 23, 55, 77};
int n = 10;
for(int i = n-1; i > 0; i--) {
    int mxIdx = 0;
    for(int j = 1; j <= i; j++)
        if(arr[mxIdx] < arr[j]) mxIdx = j;
    swap(arr[mxIdx], arr[i]);
}

or

int arr[10] = {3, 2, 7, 116, 62, 345, 1, 23, 55, 77};
int n = 10;
for(int i = n-1; i > 0; i--)
    swap(*max_eleme nt(arr, arr + i + 1), arr[i]);
```
### 버블 정렬 O(N<sup>2</sup>)
```cpp
int arr[5] = {-2, 2, 4, 6, 13};
int n = 5;
for(int i = 0; i < n; i++)
    for(int j = 0; j < n - i - 1; j++)
        if(arr[j] > arr[j + 1])
            swap(arr[j], arr[j + 1]);
```
### Merge Sort : O(N logN)
수열(정렬 된 배열)을 재귀적으로 나누고 합치는 정렬.

- **Merge Sort 순서**
1. 주어진 리스트를 2개로 나눕니다..
2. 각 리스트 정렬.
3. 규칙에 맞게 합칩니다.
<p align="center"><img src="images/mergeSort.png" width="35%"></p>

- **수열인 상태**
    ```cpp
    #include<iostream>
    using namespace std;

    int n, m;
    int a[1000002], b[1000002], c[2000002];

    int main()
    {
        ios::sync_with_stdio(0), cin.tie(0);
        cin >> n >> m;
        for (int i = 0; i < n; i++) cin >> a[i];
        for (int i = 0; i < m; i++) cin >> b[i];

        int aidx = 0, bidx = 0;
        for (int i = 0; i < n + m; i++) {
            if (bidx == m) c[i] = a[aidx++];
            else if (aidx == n)	c[i] = b[bidx++];
            else if (a[aidx] <= b[bidx])	c[i] = a[aidx++];
            else c[i] = b[bidx++];
        }
        for (int i = 0; i < n + m; i++)
            cout << c[i] << ' ';
    }
    ```

- **정렬이 필요한 상태**
    ```cpp
    #include<iostream>
    using namespace std;

    int n = 10;

    // merge 함수에서 리스트 2개를 합친 결과를 임시로 저장하고 있을 변수
    int arr[1000001], tmp[1000001];

    void merge(int st, int en) {
        int mid = (st + en) / 2;
        int lidx = st;			// a[st : mid]에서 값을 보기 위해 사용하는 index
        int ridx = mid;			// a[mid : en]에서 값을 보기 위해 사용하는 index
        for (int i = st; i < en; i++) {
            if (ridx == en) tmp[i] = arr[lidx++];
            else if (lidx == mid) tmp[i] = arr[ridx++];
            else if (arr[lidx] <= arr[ridx]) tmp[i] = arr[lidx++];
            else tmp[i] = arr[ridx++];
        }
        for (int i = st; i < en; i++) arr[i] = tmp[i];	// tmp에 임시저장해둔 값을 a로 다시 옮김
    }

    // a[st:en]을 정렬하고 싶다.
    void merge_sort(int st, int en) {
        if (en - st == 1) return;	// 길이 1인 경우
        int mid = (st + en) / 2;
        merge_sort(st, mid);		// st to mid - 1을 정렬한다.
        merge_sort(mid, en);		// mid to en - 1을 정렬한다.
        merge(st, en);

    }

    int main()
    {
        ios::sync_with_stdio(0), cin.tie(0);
        int n;
        cin >> n;
        for (int i = 0; i < n; i++)	cin >> arr[i];
        merge_sort(0, n);
        for (int i = 0; i < n; i++)	cout << arr[i] << '\n';
    }
    ```
- **Merge Sort - Stable Sort**
    우선 순위가 같은 원소들 끼리는 원래의 순서를 지킵니다. 
    <p align="center"><img src="images/stableSort.png" width="35%"></p>

### Quick Sort : 평균 - O(NlogN), 최악 - O(N<sup>2</sup>)
대부분의 정렬 알고리즘보다 빠릅니다. Pivot을 기준으로 정렬하며 해당 배열 안에서의 자리 바꿈으로 진행되기 때문에 ***cache hit rate***가 높아 속도가 빠릅니다. 추가적 공간을 사용하지 않는 정렬을 **In-Place Sort**라고 합니다.
<p align="center"><img src="images/quickSort.png" width="35%"></p>

- **Quick Sort순서**
1. Pivot을 기준으로 보다 작은 값, 보다 큰 값이 나올 때 까지 l과 r을 이동시킵니다.
2. 두 포인터가 가리키는 원소의 값을 Swap합니다.
3. l과r이 교차할 때까지 반복합니다.
4. Pivot과 r을 Swap합니다. 


```cpp
#include<iostream>
using namespace std;
 
int main()
{
	ios::sync_with_stdio(0), cin.tie(0);
    int arr[8] = {6, -8, 1, 12, 8, 3, 7, -7};
    int pivot = arr[0];
    int l = 1, r = 7;
    while(1) {
        while(l <= 3 && arr[l] <= pivot) l++;
        while(l <= r && arr[r] > pivot) r--;
        if(l > r) break;
        swap(arr[l], arr[r]);
    }
    seap(arr[0], arr[r]);
}
```

### Merge Sort VS Quick Sort
<p align="center"><img src="images/MvsQ.png" width="55%"></p>

### Counting Sort, 계수 정렬 - O(N) ~ O(N + K)
미리 만들어진 테이블에 각 수의 등장횟수를 기록합니다. 범위가 크면 사용할 수 없지만 1억 미만까지는 빠른 속도로 사용 가능합니다. ***(코테에선 천만 이하일 때만 권장)***
- **음수 포함 계수 정렬**
    ```cpp
    #include<iostream>
    #define endl '\n'
    using namespace std;

    int board[2000002];

    int main()
    {
        ios::sync_with_stdio(0), cin.tie(0);
        int n, tmp, mx = 0;
        cin >> n;
        for(int i = 0 ; i < n; i++){
            cin >> tmp;
            board[tmp+1000000]++;
            mx = max(mx, tmp+1000000);
        }
        for (int i = 0; i <= mx; i++) {
            while (board[i]--) {
                cout << i - 1000000<< endl;
            }
        }
    }
    ```
### Radix Sort, 기수 정렬 - O(D(N + K)) >> O(DN)
자릿수를 이용하여 정렬하는 알고리즘입니다.
<p align="center"><img src="images/radix.png" width="30%"></p>

### Comparison Sort vs Non - Comparison Sort
|Comparison|Non - Comparison|
|:---:|:---:|
|버블, 머지, 퀵|카운팅 라딕스|

### STL sort (for 코딩 테스트)
Quick sort기반이지만, 재귀의 깊이가 일정 이상 지속되면, 다른 알고리즘을 사용합니다. 즉, 최악의 경우에도 O(NlogN)이 보장됩니다. <br />
**Stable sort**가 아니기 때문에 동일 우선순위를 가진 원소 간에 상대적 순서가 보존되지 않을 수 있습니다. Stable sort가 필요하다면 **stable_sort**함수를 사용하면 됩니다.

```cpp
int a[5] = {1, 4, 5, 2, 7};
sort(a, a+5);

vector<int> b = {1, 4, 5, 2, 7};
sort(b.begin(), b.end());       // or sort(b.begin(), b.begin + 5)

or

// a가 b의 앞에 와야할 때 true, 그렇지 않을 때(같을 때 포함) false
// 같은 값일 때 true를 반환하면 운 좋게 통과할 수 있지만, runtime error발생 확률이 높습니다.
// 값의 복사하는 연산은 불필요하기 때문에 Reference를 보내는 것이 바람직합니다. (코딩 테스트에선 상관 없음)
bool cmp(const int& a, const int& b) {
    return a > b;
}
int a[7] = {1, 2, 3, 4, 5, 6, 7};
sort(a, a + 7, cmp);


``` 

<br />

## Greedy
지금 가장 최적인 답을 근시안적으로 택하는 알고리즘입니다. 관찰을 통해 탐색 범위를 줄인다고 볼 수 있습니다.

<br />

## Dynamic Programming
DP, 여러 개의 하위 문제를 먼저 푼 후 그 결과를 쌓아올려 주어진 문제를 해결합니다.
### 피보나치 재귀 → DP
- **재귀, O(1.628<sup>N</sup>)**
    ```cpp
    int fibo(int n) {
        if(n >= 1)
            return 1;
        return fibo(n-1) + fibo(n-2);
    }
    ```
- **DP, O(N)**
    ```cpp
    int fibo(int n) {
        int f[20];
        f[0] = f[1] = 1;
        for(int i = 2 ; i <=n; i++)
            f[i] = f[i-1] + f[i-2];
        return f[n];
    }
    ```
    중간 결과를 저장하여 이용함에 따라 극적인 차이가 발생합니다.
### DP를 푸는 과정
1. 테이블 정의하기
2. 점화식 찾기
3. 초기값 정하기
