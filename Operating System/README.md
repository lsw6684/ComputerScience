<p align="center" style="font-size:50px">
    <a href="https://github.com/lsw6684/ComputerScience">HOME</a>
</p>

***

<br />

# Operating System
- [컴퓨터 시스템](#컴퓨터-시스템)

<br />

## 컴퓨터 시스템
- 프로세서 : 처리기, 프로그램을 실행시키는 장치
- 메인 메모리 : Main Memory, 휘발성으로 램 따위를 말합니다. 명령문, 데이터 등이 있으며 데이터는 CPU로 한 문장씩 전달되어 실행됩니다.
- I/O 모듈
    - 보조기억장치 : 시스템 외부에 존재하며 주기억장치의 한정된 용량을 보조합니다.
    - 통신 장비 : 네트워크 관련 장치들
    - 터미널 : 사용자가 컴퓨터 시스템과 상호작용 하기 위해 필요한 키보드, 스크린, 프린터 따위를 말합니다.
- 시스템 버스 : 데이터의 교통수단으로 상위에서 언급한 프로세스, 메인 메모리, I/O 모듈들이 연결되어있습니다.

<p align="center"><img src="images/SystemBus.png" width="50%"></p>

**ex) 하드디스크에 들어있는 파일을 실행시킨다면**
```
1. I/O Module의 하드디스크에 있는 파일이 시스템 버스를 통해 주기억장치로 이동합니다.
2. 메인 메모리에 저장 후 프로그램이 실행되며 한 문장씩 시스템 버스를 통해 CPU로 이동됩니다.
3. 프로그램이 실행되는 동안 주기억장치의 백업 데이터가 I/O Module의 하드디스크로 이동합니다.

❗
PC - Program Counter, 다음에 실행할 명령의 주소가 들어있습니다.
IR - Instruction Register, 지금 실행 중인 명령의 내용이 들어있습니다.
PSW - Program Status Word, 비트 단위로 여러 가지 정보를 포함합니다.
    (1) Condition codes : 2bit를 사용하며 연산의 결과가 양수, 음수, 0, Overflow인지 판단합니다.
    (2) Interrupt enable/disable : 1bit를 사용하여 인터럽트가 발생 여부를 확인합니다.
    (3) Supervisor/user mode : Supervisor - OS 실행 중, user - 유저 프로그램 실행 중, 각 시기에 맞는 권한을 사용하기 위해 구분합니다.
MAR - 주기억장치에 있는 Instruction, Data는 주소로 접근이 가능합니다. 이를 위해 사용할 Instruction or Data 주소를 MAR에 저장합니다.
MBR - 주기억장치와 CPU 사이에 Instruction, Data가 오가는 중간 저장소 역할을 합니다.
AC - 범용 레지스터, 연산 결과를 임시로 저장합니다.

❗
MAR, MBR - 주기억장치와 CPU 사이에 데이터가 이동할 때
I/O AR, I/O BR - CPU와 I/O Module 사이에 데이터가 이동할 때

❗
I/O AR - MAR과 같은 역할을 합니다. 
I/O BR - MBR과 같은 역할을 합니다.
```
- **Instruction Execution :** 하위 2가지를 반복하여 프로그램을 실행합니다.
1. Fetch Stage - 메모리에서 Instruction을 가져오기.
2. Execute Stage - Instruction을 실행.
<p align="center"><img src="images/InstructionExecution.png" width="60%"></p>

**ex) 3 개의 명령 실행**
<p align="center"><img src="images/example_IE.png" width="60%"></p>

***순서***
```sql
첫 번째 Fetch Stage 시작 전, PC - 300, IR : 이전 실행 명령 주소
--------------------------------------------------------------
Fetch Stage:
1) PC -> MAR, PC++
2) memory read, MAR에 저장된 명령 -> MBR
3) MBR -> IR

Execution Stage #1:
1) 명령 분석(1)
2) IR의 주소부분(940) -> MAR
3) memory read, MAR에 저장된 데이터 -> MBR 
4) MBR -> AC                                -- 명령을 보낼 때와 다릅니다.

Execution Stage #2:
1) 명령 분석(5)
2) IR의 주소부분(941) -> MAR
3) memory read, MAR에 저장된 데이터 -> MBR
4) AC + MBR -> AC

Execution Stage #3:
1) 명령 분석(2)
2) IR의 주소부분(941) -> MAR, AC -> MBR
3) memory write, MBR -> MAR에 저장된 번지의 memory 공간 
```

- **Interrupt** 
    - 사용자의 의도와 상관 없이 정상적인 진행이 방해되는 상황을 의미합니다.
    - 프로그램은 **동시에 실행 되는 것이 아니라 CPU를 일정 시간씩 번갈아서 사용 하여 실행**됩니다.
- **Interrupt Handler :** OS의 한 부분으로 I/O의 끝처리를 합니다.

<p align="center"><img src="images/interruptCycle.png" width="60%"></p>

- **Interrupt의 종류**
    - Program Interrupt : 프로그램이 실행되는 과정에서 오버플로우, 나누기 0, 잘못된 명령을 실행하려고 할 때, 유저에게 허용되지 않은 메모리를 참조하기 등에서 발생
    - Timer Interrupt : 각 프로그램이 일정 시간동안 CPU를 사용 할 때, CPU 안에 있는 타이머가 timeout을 알려줍니다.
    - I/O Interrupt : I/O 장치가 입력 도중에 문제가 발생했음을 알려줍니다.
    - Hardware failure Interrupt : Power, Memory 등에 문제가 발생 했을 때 발생합니다.

    ※ 실제로 Interrupt를 거는 주체는 Hardware devices입니다. Hardeware devices가 CPU의 PSW 안에 있는 Interrupt enable/disable bit를 세팅합니다.

<br />

- **Interrupt Processing**
<p align="center"><img src="images/interruptProcessing.png" width="60%"></p>

- **Storage Hierarchy**
<p align="center"><img src="images/hierarchy1.png" width="50%"><img src="images/hierarchy2.png" width="50%"></p>

- **캐시 메모리**
    - 메인메모리와 CPU 사이에 존재합니다.
    - Processor와 CPU와 속도가 비슷하며 **굉장히 빠르다**고 할 수 있습니다.
    - 메인메모리에서 명령을 한 줄씩 가져오고 실행하는 것이 원칙이지만, 속도 향상을 위해 더욱 가까운(빠른) **캐시 메모리에 일부를 가져다 놓고 실행**합니다.
    - 캐시 메모리의 **크기는 매우 작기 때문에** 실행할 프로그램들의 데이터들을 모두 가져올 수는 없습니다.
    - **국부성, Locality** - 전체가 아닌 일부를 반복해서 사용하는 경향을 의미합니다.
    - OS에서 관리하는 것이 아니기 때문에 **(Hardware적인 관리) 속도가 빠릅니다.**