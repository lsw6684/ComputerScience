<p align="center" style="font-size:50px">
    <a href="https://github.com/lsw6684/ComputerScience">HOME</a>
</p>

***

<br />

# Natural Language Processing
- [Foundation](#foundation)
- [Machine Learning with scikit-learn](#machine-learning-with-scikit-learn)





## Foundation
**SciPy** : Scientific Computing으로 수학, 과학, 그리고 공학 관련된 연산을 지원합니다. MATLAB에 대응하기 위한 오픈소스 Computing Tool이라고 생각합니다.
- **array**
    ```python
    import numpy as np
    # From a composite data (list or tuple, not set and dictionary)
    A = np.array([3, 29, 82])                   #리스트
    B = np.array(((3., 29, 82), (10, 18, 84)))  #튜플, "."은 float 64 의미. 
    C = np.array([[3, 29, 82], [10, 18, 84]], dtype=float)
    D = np.array([3, 29, 'choi'])
    E = np.array([[3], [29], [82]])

    # ndim = 차원, size = element 개수, shape = 행렬. 왜 1이 안나올까
    # dtype = 데이터타입. 하나를 설정해 놓으면 모두 바뀐다 - homogenous
    print(A.ndim, A.size, A.shape, A.dtype)     # 1 3 (3,) int 32
    print(B.ndim, B.size, B.shape, B.dtype)     # 2 6 (2, 3) float64
    print(C.ndim, C.size, C.shape, C.dtype)     # 2 6 (2, 3) float64
    print(D.ndim, D.size, D.shape, D.dtype)     # 1 3 (3, 1) 유니코드로 나오고 
    print(D) # ['3' '29' 'choi']정수들도 텍스트로 변환
    print(E.ndim, E.size, E.shape, E.dtype)     # 2 3 (3, 1) int32

    # Using initialization functions
    F = np.zeros((3, 2))            # Create a 3x2 array filled with 0 (default: float 64)
    G = np.ones((3, 2))             # Create a 2x3 array filled with 1
    H = np.eye(3, dtype=np.float32) # Create a 3x3 identity matrix (single-precision)
    I = np.empty((3, 2))            # zeros((3, 2)) but the elemets are 1
    J = np.empty((0, 9))            # [] width size of (0, 9). just space.
    K = np.arange(0, 1, 0.2)        # 0이상 1 미만, 0.2(step)차이로 나열
    L = np.linspace(0, 1, 5)        # 0이상 1 이하, 5개로 나누기
    M = np. random.random((3, 2)) # == np.random.uniform(size=(3, 2)) cf. normal()    
    ```
- **Indexing and slicing**
<p align="center"><img src="images/indexingSlicing.png" width="650"></p>


- **Matplotlib** : 2차원 그래프를 그려주기 위함입니다. 3차원도 지원 하지만, 별로...
    ```python
    import matplotlib.pyplot as plt
    import numpy as np

    xs = np.arange(-4, 10, 0.001) # -4이상 10미만까지 0.001간격으로 생성
    ys = [0.1*x**3 - 0.8*x**2 - 1.5*x +5.4 for x in xs]
    yt = [-3.5*x + 7 for x in xs]

    fig = plt.figure()              # figure는 그림 단위. plot을 관리
    trim = fig.add_subplot(1, 1, 1) # subplot은 plot 1개를 의미. 1x1 비율로, 첫 번째 plot
    trim.set_aspect('equal')        # 지금은 plot이 1개 뿐이라 마지막 매개변수는 1밖에 안됨.

    plt.plot(xs, ys, color='r', label = 'y')
    plt.plot(xs, yt, color='b', label='tangent line')

    plt.grid()   # 그리드
    plt.legend() # 라벨
    plt.show()   # 화편에 출력.
    ```
<p align="center"><img src="images/matplotlib_basic.png" width="180"></p>

- **SymPy** : 수학적 계산을 위한 라이브러리입니다.
<p align="center"><img src="images/sympy_basic.png" width="600"></p>

<p align="center"><img src="images/factorize.png" width="700"></p>

- **NumPy** : 다차원 벡터, 행렬을 쉽게 처리할 수 있는 빠른 속도의 라이브러리입니다. array형태의 데이터를 효율적으로(속도↑ 메모리↓) 처리합니다.
    <p align="center"><img src="images/행렬.png" width="600"></p>
    Numpy.array는 **homogeneous**, 제차형 데이터 타입만 포함할 수 있습니다. 
    
- **Data types**

    대소문자를 구분합니다.
    ```python
    profs = [
    'My name is Choi and my E-mail is sunglok@seoultech.ac.kr.',
    'My name is Kim and my e-mail address is jindae.kim@seoultech.ac.kr.'
    ]
    print(['e-mail' == prof for prof in profs ])        # [False, False] cf. matching
    print(['e-mail' in prof for prof in profs])         # [False, True] cf. searching
    print(['e-mail' in prof.lower() for prof in profs]) # [True, True] cf.
    print([prof.find('e-mail') for prof in profs])      # [-1, 22]
    print([prof endswith('.') for prof in profs])       # [True, True] cf. startswith
    ```
    - **fnmatch**
        - \* : matches everything
        - ? : matches any single character
        - [seq] : matches any character in seq
        - [!seq] : matches any character not in seq 
        
            **fnmatch는** 대/소문자를 구별하지 않고, **fnmatchcase**를 사용해야 대/소문자를 구별합니다.
        ```python
        import fnmatch

        profs = [
        'My name is Choi and my E-mail is sunglok@seoultech.ac.kr.',
        'My name is Kim and my e-mail address is jindae.kim@seoultech.ac.kr.'
        ]

        # for a single string
        print([fnmatch.fnmatch(prof, 'e-mail') for prof in profs])
        print([fnmatch.fnmatch(prof, '*e-mail*') for prof in profs])
        print([fnmatch.fnmatchcase(prof, '*e-mail*') for prof in profs])
        print([fnmatch.fnmatchcase(prof, '*[Ee]-mail*') for prof in profs])

        # for a list of strings
        print(fnmatch.filter(profs, '*e-mail*'))
        print(fnmatch.filter(profs, '*ch?i*'))        
        >>>
            [False, False]
            [True, True]
            [False, True]
            [True, True]
            ['My name is Choi and my E-mail is sunglok@seoultech.ac.kr.', 'My name is Kim and my e-mail address is jindae.kim@seoultech.ac.kr.']
            ['My name is Choi and my E-mail is sunglok@seoultech.ac.kr.']

        ```
- **정규식 Regular Expression** <br />
search를 위한 string 패턴입니다. 복잡한 문자열을 처리할 때 사용하는 기법으로, Python만의 고유 문법이 아니라 문자열을 처리하는 모든 곳에서 사용됩니다. 정규 표현식을 배우는 것은 Python을 배우는 것과는 또 다른 영역의 과제라 할 수 있습니다.
<p align="center"><img src="images/re1.png" width="1000"></p>

<p align="center"><img src="images/re2.png" width="500"></p>

<p align="center"><img src="images/re3.png" width="500"></p>

<p align="center"><img src="images/re4.png" width="1500"></p>

## Machine Learning with scikit-learn