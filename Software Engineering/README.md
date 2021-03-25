<p align="center" style="font-size:50px">
    <a href="https://github.com/lsw6684/ComputerScience">HOME</a>
</p>

***

<br />

# Software Engineering
- [User Interface](#user-interface)
- [Cloud Service Model](#cloud-service-model)

<br />

## User Interface
UI는 사용자와 시스템 사이에서 의사소통을 할 수 있도록 고안된 물리적, 가상의 매개체입니다. 일반적으로 SW를 사용할 때 접하게 되는 화면입니다.
- **UI 유형**
    - **CLI Command Line Interface** : 정적인 텍스트 기반 인터페이스로 명령어를 입력하여 사용합니다. `cmd`
    - **GUI Graphical User Interface** : 사용자가 문자 명령어 대신 이미지를 사용해 전자기기와 상호 작용할 수 있도록 하는 일종의 사용자 인터페이스이며, 그래픽 반응 기반 인터페이스로 마우스나 전자펜을 사용합니다.
    - **NUL Natural User Interface** : 직관적인 사용자 반응 인터페이스로 신체 부위나 터치, 음성 등으로 사용합니다.
    - **OUI Organic User Interface** : 유기적 상호작용 인터페이스로 현실에 존재하는 모든 사물이 입출력장치가 될 수 있습니다.
- **UI 설계 원칙**
    - **직관성** : 누구나 쉽게 이해하고 사용할 수 있어야 합니다. `쉬운 검색, 사용성, 일관성`
    - **유효성** : 정확하고 완벽하게 목표가 달성될 수 있도록 제작되어야 합니다 `쉬운 오류 처리 및 복구`
    - **학습성** : 초보와 숙련자 모두 쉽게 배우고 사용할 수 있게 제작되어야 합니다. `쉬운 학습과 기억, 쉬운 접근`
    - **유연성** : 사용자 인터랙션을 최대한 포용하고 실수를 방지할 수 있도록 합니다. `오류 예방 및 감지, 실수 포용`

- **UI 설계 지침**
    - **사용자 중심** : 사용자가 이해하기 쉽고 편하게 사용합니다.
    - **일관성** : 버튼이나 조작 방법을 쉽고 빠르게 습득하도록 설계합니다.
    - **단순성** : 조작 방법을 간단하게 하여 인지적 부담을 최소화합니다.
    - **결과 예측 가능** : 작동시킬 기능을 보고 결과 예측이 가능하게끔 합니다.
    - **가시성** : 주요 기능을 메인 화면에 노출하여 쉬운 조작이 가능합니다.
    - **표준화** : 디자인을 표준화하여 기능 구조의 선행 학습 이후 쉽게 사용 가능합니다.
    - **접근성** : 사용자 직무, 연령, 성별 등이 고려된 다양한 계층을 수용합니다.
    - **명확성** : 사용자가 개념적으로 쉽게 인지합니다.
    - **오류 발생 해결** : 사용자가 오류에 대한 상황을 정확하게 인지할 수 있습니다.
    
<br />

## Cloud Service Model
- **SaaS Software as a Service**<br />
    클라우드 환경에서 동작하는 응용 프로그램을 클라이언트에게 서비스하는 모델로 `on-demand software`로도 불립니다. 소프트웨어 및 관련 데이터는 중앙에 호스팅되고 사용자는 웹 브라우저 등의 클라이언트를 통해 접속하는 형태의 소프트웨어 전달 모델입니다.
- **PaaS Platform as a Service**<br />
    애플리케이션을 개발, 실행, 관리할 수 있게 하는 플랫폼을 서비스로 제공하는 모델입니다. 개발자가 맞춤형 애플리케이션을 개발하고 구축할 수 있는 프레임워크를 제공합니다. 스토리지 및 네트워킹은 엔터프라이즈 또는 타사 공급자가 관리할 수 있으며 개발자는 응용 프로그램 관리를 유지할 수 있습니다. 비용면에서 [IaaS](#iaas-infrastructure-as-a-service)보다 비쌉니다.<br />
    `AWS Elastic Beanstalk, Windows Azure, Heroku`
- ## IaaS Infrastructure as a Service
    서버, 네트워크, 스토리지등을 가상화하여 필요에 따라 인프라 자원을 사용할 수 있게 만드는 서비스 모델입니다. OS, Web Server, DB 등 버전까지 선택하여 개발환경을 구축, 즉 컴퓨터 환경만을 빌려서 사용하는 것입니다.<br />
    `AWS EC2, Google Cloud Platform, Azure Virtual Machines, Naver Cloud Platform`