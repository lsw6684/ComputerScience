<p align="center" style="font-size:50px">
    <a href="https://github.com/lsw6684/ComputerScience">HOME</a>
</p>

***

# Reinforcement Learning
- [Introduction to Reinforcement Learning](#introduction-to-reinforcement-learning)

<br />

## Introduction to Reinforcement Learning
- ML : Machine Learning
    - 프로그램이 데이터로부터 자동으로 학습을 합니다.
    - 데이터의 일부 example들을 일반화여 특정 문제를 해결하는 알고리즘입니다.
    - 모델을 만들기 위한 샘플 데이터를 Training data라고 부릅니다.
- ML 알고리즘의 종류
    - 지도 학습 Supervised Learning : input(X) & desired output(Y)을 포함하는 데이터를 기반으로 수학적 모델(f)을 만듭니다.
        - Regression : data point를 Generalization 하여 ax + b 형태의 함수 f,**연속적인** function line을 만들어 **real value**를 예측합니다.
        - Classification : input이 **어떤 class**에 속하는지 예측합니다.
    - 비지도 학습 Unsupervised Learning : 데이터에 input(X)만이 있으며 **desired output(Y)이 없습니다**. 데이터의 패턴, 구조를 찾아내어 그룹핑이나 **클러스터링**을 합니다.

    - 강화 학습 Reinforcement Learning : 특정 환경에서 Agent(SW or HW)가 현재의 상태를 인식하여, 누적된 보상을 최대화하는 행동 혹은 행동 순서를 선택하는 방법입니다.
        - ex) ```강아지에게 캐치볼 하는 것을 가르칩니다. 하지만 명시적으로 가르칠 수 없으니 공을 던지고 다시 가져오는 것을 성공할 때마다 간식을 줍니다. 그리고 실패 하면 간식을 주지 않습니다. 이 과정을 반복하면, 강아지는 어떤 Action을 해야 간식을 얻을 수 있는지 알게됩니다.```