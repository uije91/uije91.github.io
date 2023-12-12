---
title:  "컴퓨터 구조"
category: computerScience
typora-root-url: ../
toc: true
toc_sticky: true
---



## <br>컴퓨터 시스템

- 하드웨어(Hardware): CPU, Memory, Storage, Network등
- 소프트웨어(Software): 운영체제와 응용 프로그램

### <br>폰노이만 구조

- Memory에 프로그램과 데이터가 저장
- 하나씩 꺼내어 CPU:Arithmetic Logic Unit로 연산
  - 입력 -> 메모리 -> CPU -> 메모리 -> 출력

<img src="/../images/2023-12-10-computer01/Von_Neumann.png" alt="Von_Neumann" style="zoom: 20%;" />

### <br>컴퓨터 주요 구성 요소

- CPU(중앙처리장치, Central Processor Unit)
  - 연산: ALU(Arithmetic Logic Unit)
    - 산술 연산(Arithmetic Operation) 과 논리 연산(Logic Operation) 수행
  - 제어: Control Device
    - IO Device(입출력장치), Memory, ALU 동작 제어
- Memory(**코드**와 **데이터**를 저장하는 장치)
  - 프로그램과 프로그램 수행에 필요한 데이터를 저장
  - 내부 기억장치 (주기억장치)
    - CPU 안에 레지스터(register), 캐쉬(cache memory)
    - DRAM등 메모리 (램, RAM, DDR4)
  - 외부 기억장치 (보조기억장치)
    - SSD, HDD
- IO Devices(입출력 장치)
  - 입력 장치: 마우스, 키보드, 터치패드 등
  - 출력 장치: 모니터, 프린터, 스피커 등
- Bus(버스)
  - CPU, Memory, IO Devices를 연결 해주는 장치
  - 구성 요소들 간의 데이터를 송수신에 사용

### <br>비트

- 컴퓨터는 이진수 체계( 0 또는 1)를 사용하여 숫자,문자 등을 표현

### <br>논리 연산

- `OR`, `A+B`
- `AND`, `AB`
- `NOT`, `A'`
- `NAND`, `(AB)'`
- `NOR`, `(A+B)'`
- `XOR`, `A⊕B`



### <br>이진수의 덧셈

- `0 + 0, S=0, C=0`
- `0 + 1, S=1, C=0`
- `1 + 0, S=1, C=0`
- `1 + 1, S=0, C=1`, 이 경우 Carry 발생
- `S(sum)`는 `XOR`, `C(carry)`는 `AND`

#### <br>반가산기(Half Adder) 

- 두 bit를 덧셈하는 가산기를 의미
- `XOR`와 `AND`로 구성된 조합논리회로
- 두 bit를 더해서 `Sum`와 `Carry`를 출력
- 이전 단계에서의 `Carry`는 고려하지 못함

#### <br>전가산기(Full Adder)

- 반가산기 2개의 조합으로 구성
- 이전 단계에서의 `Carry`를 고려할 수 있다.
- 두 bit와 carry bit 값을 입력으로 받아서 `Sum`와 `Carry`을 출력
- **전가산기 여러개를 연결해서 조합하면 여러 자리의 비트를 계산할 수 있다.**

### <br>오실레이터(Oscillator)

- 반복적인 또는 주기적인 시간 변화 신호를 생성하는 전자 회로
- `0`과 `1`을 반복, 클럭을 만들 수 있다.
- **CPU는 클럭 주기에 맞춰 명령을 수행한다.**
  - 주기(Cycle): 한 사이클에 필요한 시간
  - frequency: 단위 `hertz`, 1초에 클럭이 몇 번 발생하는지

### <br>플립플롭(Flip-Flop)

- 데이터를 저장하는 조합논리회로
- Memory에 사용

#### <br>RS Flip-Flop

- Input: `R(Reset)`,`S(Set)`
- Output: `Q`, `Q'`
- S와 R이 1인 상태는 피하도록 설계

<img src="/../images/2023-12-10-computer01/rsFlipflop.png" alt="rsFlipflop" style="zoom:60%;" />

#### <br>Level-triggered Flip-Flop

- Input으로 `Hold That Bit` 추가: `R(Reset)`과 `S(Set)`에 같이 영향을 준다(`And`)
  - `Hold That Bit`는 클럭 신호
- `And`이므로`Hold That Bit = 1` 일 때만 `Data = 1`

#### <br>D-Type Flip-Flop

- `R/S` 둘 다 1일 경우를 피하도록 설계
- Input을 `D(Data)` 하나로 변경, `NOT` 게이트로 설계

#### <br>1bit latch

- `Level-triggered D type flip-flop`
- **1bit를 일시적으로 저장할 수 있는 메모리**

#### <br>8bit latch

- `3-to-8 decoder`와 `8-to-1 selector`로 구성(Address)

  - 8-to-1 selector
    - 8bit 데이터에서 특정 bit 값만 출력
    - 3bit만 있으면 됨,  2<sup>3</sup> = 8

  - 3-to8 decoder
    - 8개의 출력 중 단 하나의 출력 이외에는 0
    - 8개 중 단 하나에만 값을 쓸 때 사용

- 데이터를 읽고 쓸 수 있는 Address
- 이 회로가 바로 `RAM(Random Access Memory)`
- `클럭=1`일 때, 8 bit Data Inputs이 8 bit Data Outputs에 저장
- `클럭=0`일 때, 8 bit Data Outputs 값 유지

### <br>RAM(Random Access Memory)

- 데이터를 저장할 수 있다.
- 특정 공간에 데이터를 저장하거나 읽기가 가능하다.
- **순차 접근이 아닌 주소 지정을 통해 특정 공간에 접근할 수 있다.**
- `8 X 1 RAM`: 8개 비트 중 1개의 비트를 쓰고 읽을 수 있다.

#### <br>RAM Array

- 2개 이상의 RAM으로 구성
- `8 X 1 RAM`을 어떻게 조합하냐에 따라 `8 X 2 RAM`이 될 수도 있고 `16 X 1 RAM`이 될 수도 있다.



### <br>누산기(Accumulator)

- `8 bit Adder` 와 `8 bit Latch`로 구성
- 값을 더하고 더한 값을 저장할 수 있다.



### <br>메모리 계층 구조

- 상위(`용량 작음, 속도 빠름, 가격 비쌈`)
- 하위(`용량 큼, 속도 느림, 가격 쌈`)

<img src="/../images/2023-12-10-computer01/memory.png" alt="memory" style="zoom:70%;" />

### <br>DMA(Direct Memory Access)

- CPU가 캐쉬까지는 데이터를 가져오는데 관여하지만(Instruction Fetch) 메모리, SSD에서 데이터를 가져오는데까지 관여하면 CPU 활용도가 낮아진다
- DMA라고 만들어서 메모리, SSD에서 데이터를 관리하면 CPU는 이 시간을 명령 실행에 더 쓸 수 있다.

### <br>Program Counter(PC)

- **다음에 실행할 명령어의 주소를 가리키는 레지스터**
- n-bit Counter: 1씩 증가하는 조합논리회로

### <br>CPU 기본 구조

- PC(Program Counter): 다음 실행할 명령어 주소를 가리키는 레지스터
- IR(Instruction Register): 가장 최근에 인출한 명령어 보관 레지스터
- 누산기(Accumulator): 데이터 일시 보관 레지스터
- MAR(Memory Address Register): CPU가 메모리를 참조하기 위해 데이터 주소를 보관하는 레지스터
- MBR(Memory Buffer Register): CPU가 메모리로부터 읽거나, 저장할 데이터 자체를 보관하는 레지스터

### <br>CPU 명령어 실행 순서

1.  Instruction Fetch: 실행할 명령어를 메모리에서 읽어 CPU로 가져옴 
   - PC가 가리키는 주소를 MAR에 보냄 
   - MAR에 적힌 주소를 메모리에서 읽어서 MBR에 보냄 
   - MBR에 있는 명령어를 IR에 저장 
   - 다음 명령어를 가리키도록 PC는 주소값 증가 
2. Instruction Decode: 인출한 명령어에 포함된 데이터 가져오고 명령어 해독 
3. Instruction Execution: 명령어 실행 
   - MBR의 데이터와 Accumulator의 데이터로 연산 후, Accumulator에 저 장 
4. Write Back: 실행 결과를 저장

### <br>파이프라인

- CPU의 성능을 높이는 기법
- **하나의 작업에 필요한 일을 세부적으로 나누어서 동시에 다른 세부작업을 실행하는 기법**

### <br>CISC vs RISC

> CPU 명령어를 정의하는 2가지 전략

#### CISC(Complex Instruction Set Computer)

- 하나의 명령어 실행으로 가능한 한 많은 작업을 수행
- 복합 명령어 수행으로 인한 CPU 로직 회로 복잡도 증가
- CISC 특징
  - 명령어의 포맷이나 길이에 관한 규칙이 없음
  - 하나 이상의 사이클로 명령어(세부 작업) 실행
  - 전체 명령이 얼마나 걸릴지 시간 예측이 어려움
- 대표적인 CISC CPU: 인텔, AMD

#### RISC(Reduced Instruction Set Computer)

- 간단한 명령어를 조합해서 명령 수행
- RISC 특성
  - 명령어의 포맷과 길이 고정
  - 하나의 사이클로 명령어(세부 작업) 실행
  - 전체 명령 시간 예측이 가능
- 전력 소모가 적음
- 대표적인 RISC CPU: ARM, 스마트폰, 임베디드, IOT 기기