<p align="center" style="font-size:50px">
    <a href="https://github.com/lsw6684/ComputerScience">HOME</a>
</p>

***

<br />

# Operating System
- [**컴퓨터 시스템**](#컴퓨터-시스템)

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
- Instruction Execution : 하위 2가지를 반복하여 프로그램을 실행합니다.
1. Fetch Stage - 메모리에서 Instruction을 가져오기.
2. Execute Stage - Instruction을 실행.
<p align="center"><img src="images/InstructionExecution.png" width="40%"></p>

**ex) 3 개의 명령 실행**
<p align="center"><img src="images/example_IE.png" width="40%"></p>

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