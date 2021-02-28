# ALGORITHM (Including Data Structure)
- [ALGORITHM (Including Data Structure)](#algorithm-including-data-structure)
  - [시간복잡도 & 공간복잡도](#시간복잡도--공간복잡도)


</br>

## 시간복잡도 & 공간복잡도
- 시간복잡도

    ```cpp
    int func(int arr[], int n) {
        int cnt = 0;                    // cnt 1번
        for(int i = 0; i < n; i++)      // for( 1번; n번; n번 )
            if(arr[i] % 5 == 0) cnt++;  // if(1번, 1번) 1번
        }
        return cnt;                     // 1+1+n(2+2+1)+1 = 5n+3                                   
    }   
    ```
    n이 100만이면 약 500만의 연산이 필요하여 1초 안에 **가능**.

    n이 10억이면 약 50억번의 연사이 필요하여 1초 안에 **불가능**.

    ※ **5n+3 → n에 비례**한다고 표현합니다.