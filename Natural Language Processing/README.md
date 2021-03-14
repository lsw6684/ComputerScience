<p align="center" style="font-size:50px">
    <a href="https://github.com/lsw6684/ComputerScience">HOME</a>
</p>

***

<br />

# Natural Language Processing
- [**Foundation**](#foundation)






## Foundation
### **SciPy** : Scientific Computing으로 수학, 과학, 그리고 공학 관련된 연산을 지원합니다.

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

- Data types

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
- **정규식 Regular Expression** : search를 위한 string 패턴입니다.
