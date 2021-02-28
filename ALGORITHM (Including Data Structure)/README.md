# ALGORITHM (Including Data Structure)
  - [C++ 입출력 속도 향상](#C++-입출력-속도-향상)
  - [시간복잡도 & 공간복잡도](#시간복잡도--공간복잡도)



<br />

## C++ 입출력 속도 향상
- std::endl → **"\n"** : endl은 버퍼를 비우고 출력을 진행하기 때문에 상당한 시간을 요구합니다. \n을 사용하는 것이 **월등히 빠르다**고 할 수 있습니다.

    `#define endl "\n"`을 상단에 정의하면 \n을 endl로도 표현할 수 있습니다. (전역변수 std 사용 시 주의❗)
- ios::sync_with_stdio(0), cin.tie(0) - 메인함수 안에 선언
    - ios::sync_with_stdio(0) : cin과 cout은 stream상에서 분리되어 있기 때문에 동기화할 시간이 필요합니다. 그렇기 때문에 앞에서 언급된 문장을 선언함으로써 동기화를 끊어야 합니다. (해당 방법을 사용할 시 scanf/printf를 사용하면 안 됩니다❗)
    - cin.tie(0) : cin은 endl과 같은 개념으로 버퍼를 사용하기 때문에 속도가 느립니다. 이러한 과정을 생략하기 위해 사용됩니다.
- using namespace std - 전역 : 많은 사람들이 전역변수를 사용하는 것은 프로그래밍 관점으로 봤을 때 충돌을 야기할 수 있으며 지양해야 하는 부분이라고 말합니다. 저 또한 그렇게 생각합니다. 하지만, 코딩 테스트를 위한 코딩은, 남에게 보여주거나 유지보수를 고려해야 하는 클린 코딩이 아니고 **속도와 순간의 편리성이 우선**이라고 생각합니다.

<br />

## 시간복잡도 & 공간복잡도
- **시간복잡도(Time Complexity) :** 입력의 크기와 문제를 해결하는데 걸리는 시간의 상관관계
  - 빅오표기법 (Big-O Notation) : 주어진 식을 값이 가장 큰 대표항만 남겨서 나타내는 방법
    - O(N) : 5N + 3, 2N + 10lgN, 10N
    - O(N²) : N² + 2N + 4, 6N² + 20N, 10lgN
    - O(NlgN) : NlgN + 30N + 10, 5NlgN + 6
    - O(1) : 5, 16, 36
<p align="center"><img src="./../images/timeComplexity.png" width="50%"></p>

<p align="center"><img src="./../images/bigO.png" width="50%"></p>

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