> CPU의 정상적인 프로그램 실행을 방해하는 행위

프로그램을 실행하는 도중에 예기치 않은 상황(입출력, 우선 순위 연산 등)이 발생할 경우, 현재 실행 중인 작업을 즉시 중단하고 발생된 상황에 대한 우선 처리가 필요함을 CPU에게 알린다. 

- 외부/내부 인터럽트: `CPU의 하드웨어 신호에 의해 발생`
- 소프트웨어 인터럽트: `명령어의 수행에 의해 발생`

<br>

### 외부 인터럽트

1. 전원 이상 인터럽트: 전원 공급이 중단되는 경우, CPU에 인터럽트 요청
2. 타이머 인터럽트: 타이머가 일정한 시간 간격으로 CPU에게 인터럽트 요청 (하나의 프로그램이 CPU 자원을 너무 오랫동안 점유하지 못하도록)
3. 입출력 인터럽트: CPU가 I/O장치(키보드, 마우스, 프린터 등)에게 일을 맡기거나, I/O장치가 CPU에게 정보를 전달해 줄 때  인터럽트 요청

<br>


### 내부 인터럽트 (Exception Interrupt, Trap)

CPU 코어 내부에서 프로그램이 실행되면서 인터럽트 요청되는 경우

1. Division by zero
2. Overflow/Underflow
3. 기타 프로그램 Exception

<br>

### 소프트웨어 인터럽트

1. 프로그램 처리 중 명령어에 의해 발생하는 경우 

<br>

### 동작 순서

1. **인터럽트 요청**
    
    입출력장치에서 CPU에 인터럽트 요청 신호(INTR)를 보낸다.
    
    CPU는 실행 사이클을 끝내고 인터럽트 요청신호를 확인한다. 인터럽트 요청을 확인 후 인터럽트 가능 플래그(IE)를 통해 현재 인터럽트를 받아들일 수 있는지 확인한다.
    
2. **프로그램 실행 중단**
    
    인터럽트를 받아들일 수 있다면 현재 실행하던 프로그램을 중단
    
3. **현재 실행 중인 프로그램 상태 보관**
    
    Program Counter와  Status Register를 스택에 저장
    
4. **인터럽트 처리 루틴 실행**
    
    인터럽트를 요청한 장치를 식별한다. 
    
5. **인터럽트 서비스 루틴 처리** 
    
    CPU는 Interrupt Vector를 참조하여 인터럽트 서비스 루틴 실행한다. (ISR: 인터럽트가 발생한 경우 인터럽트 처리를 위한 프로그램으로 일반적으로 메모리에 저장되어 있다.)
    
6. **상태 복구** 
    
    ISR 실행이 끝나면 스택에 저장한 PC와 SR값을 복구하여 실행 중이던 프로그램 실행을 재개한다.

<br>

### 관련 예시

- 구글 검색창을 클릭 후 빈칸에 커서가 깜빡이고 있다. 이때 검색어를 입력하면 컴퓨터 내부에서 어떤일이 발생할까?
    
    사용자 입력 → 외부 인터럽트(I/O 인터럽트) 발생 → CPU 인지 → CPU: 작업중이던 상태 저장 → 해당 인터럽트 처리 → 상태 복구 및 중단되었던 작업 재개

<br>