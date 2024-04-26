# 중앙처리장치(CPU) 작동원리

# CPU

## 사전적 의미

컴퓨터에서 기억, 해석, 연산, 제어 (4대 주요 기능)를 담당하는 장치

## 구성 요소

1. 산술논리연산장치(ALU - Arithmetic Logic Unit) : 산술 및 논리 연산 수행하는 장치, 연산에 필요한 데이터를 레지스터와 교환
2. 제어유닛(Control Unit) : 명령어의 순서와 수행을 제어하는 장치, 주기억장치(RAM)에서 프로그램 명령어를 꺼내서 해독 후 기억장치, 연산장치, 입출력장치로 보냄
3. 레지스터(Register) : 연산의 중간 결과와 작업 상태를 저장하는 장치(고속 기억장치), 명령어 주소, 코드, 연산에 필요한 데이터 등을 저장.
    
    (용도에 따라 1. 범용 레지스터 / 2. 특수목적 레지스터로 나뉜다. )
    
    <aside>
    💡 **<특수 목적 레지스터>**
    - MAR(메모리 주소 레지스터) : 읽기/쓰기 연산을 수행할 주기억장치 “주소” 저장
    - PC(프로그램 카운터) : 다음 차례에 수행할 명령어 “주소” 저장
    - IR(명령어 레지스터) : 현재 실행 중인 “명령어” 저장
    - MBR(메모리 버퍼 레지스터) : 주기억장치에서 읽어오거나 저장할 데이터 “임시” 저장
    - AC(누산기) : 연산 결과 임시 저장
    
    </aside>
    

## CPU 동작 과정

1. I/O Device에서 입력받은 데이터 or 보조기억장치(HDD/SSD)에 저장된 프로그램을 읽어옴
2. 주기억장치(RAM)에 저장된 프로그램 명령어(Instruction)와 데이터를 읽고 처리하여 다시 주기억장치(RAM)이 저장
3. 주기억장치(RAM)는 처리 결과를 보조기억장치(HDD/SSD)에 저장하거나 I/O Device를 통해 유저에게 전달

(Control Unit은 1~3의 과정을 순서대로 실행하도록 각 장치를 제어)

<aside>
💡 <RAM(Random Access Memory)의 특징>
- 컴퓨터의 주기억장치
- 운영에 필요한 데이터 처리
- 모든 임의의 주소에 동일한 시간에 접근 가능
- 전원이 공급되지 않으면 데이터가 삭제되는 휘발성 메모리
- CPU가 데이터를 읽거나 저장하기 위해 사용하는 용도
- SRAM, DRAM, SDRAM 등… 다양한 메모리 종류가 존재(추후에 자세하게 설명 예정)

</aside>

<aside>
💡 <ROM(Read Only Memory)의 특징>
- 추후 작성 예정

</aside>

<aside>
💡 <주기억장치 & 보조기억장치>
- 추후 작성 예정

</aside>

<aside>
💡 <명령어 세트란?>
CPU가 실행할 명령어의 집합

명령어 세트의 구성 요소
1. 연산코드(Operation Code) : 실행할 연산 → 기능
2. 피연산자(Operand) : 필요한 데이터 or 주소 → 저장 데이터

</aside>

## 명령어 사이클

CPU가 주기억 장치에서 한 번에 하나의 명령어를 인출하여 실행하는데 필요한 일연의 활동

1. 인출
2. 실행
3. 간접
4. 인터럽트

로 이루어져있음.

### 1. 인출 사이클

- PC(Program Counter)에 저장된 주소를 MAR(Memroy Address Register)에 전달
- 전달한 주소를 토대로 주기억장치(RAM)의 주소에서 명령어(Instruction) 인출
- 인출한 명령어를 MBR(Memory Buffer Register)에 전달
- **다음 명령어 인출을 위해 ⭐️PC값 증가⭐️ (매우 중요)**
- MBR(Memory Buffer Register)에 저장된 내용을 명령어 레지스터(IR)에 전달

```jsx
T0 : MAR ← PC
T1 : MBR ← M[MAR], PC ← PC+1
T2 : IR ← MBR
```

### 2. 명령어 실행 사이클

(ex. ADD addr)

```jsx
T0 : MAR ← IR(Addr)
T1 : MBR ← M[MAR]
T2 : AC ← AC + MBR
```

- 현재 IR(명령어 레지스터)에는 MBR(메모리 버퍼 레지스터)의 값이 이미 저장됨.
- 따라서 AC(누산기)에 MBR을 더해주면 끝.

(ex. LOAD addr)

```jsx
T0 : MAR ← IR(Addr)
T1 : MBR ← M[MAR]
T2 : AC ← MBR
```

- 기억장치에 있는 데이터를 AC로 이동하는 명령어

(ex. STA addr) - store

```jsx
T0 : MAR ← IR(Addr)
T1 : MBR ← AC
T2 : M[MAR] ← MBR
```

- AC에 있는 데이터를 기억장치로 저장하는 명령어

(ex. JUMP addr)

```jsx
T0 : PC ← IR(Addr)
```

- PC값을 IR의 주소값으로 변경하는 분기 명령어
