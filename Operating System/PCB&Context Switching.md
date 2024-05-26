### 들어가기전에 ..

OS의 역할?

1. 프로세스 관리 ( 프로세스, 스레드, 스케줄링, IPC 통신 ..)
2. 저장장치 관리(메모리 ..)
3. 네트워킹 ( TCP/IP 등 프로토콜)
4. 사용자 관리 (계정, 접근권한 ..)
5. 디바이스 드라이버 (장치들)

여기서 프로세스 관리는 , 프로세스가 여러개일 때 **현재 CPU를 점유해야 할 프로세스를 결정하고, CPU를 프로세스에 할당**하는 일 등을 말한다. 

이때, CPU는 각각 프로세스들이 누군지 알아야 관리를 할 수 있겠지?

프로세스를 구분할 수 있게 하는 것이 바로`Process Metadata`이다.

```
💡 프로세스 ID, 프로세스 상태, 프로세스 우선순위, CPU Registers의 값들, Owner, CPU 사용량, 메모리 사용량 등의 정보를 가지고 있음
```

이 `Process Metadata` 는 프로세스가 생성되면 `PCB(Process Control Block)`에 저장된다.

## 💡 Process Control Block

프로세스의 메타데이터들을 저장 ! 1 PCB → 1 Process 정보

![image](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/83461362/3c43ab34-5b96-433c-996d-01ce2d1eba08)

- Process ID
- Process State: 프로세스 스케줄링 상태
- Process Priority
- 프로세스 권한 : 컴퓨터 자원 또는 I/O 디바이스에 대한 권한 정보
- Program Counter: 프로세스에서 실행해야 할 다음 명령어 주소에 대한 포인터
- CPU Register: 프로세스의 레지스터 상태를 저장하는 공간, 레지스터의 값들을 기억시킴
- CPU 스케줄링 정보: CPU 스케줄러에 의해 중단된 시간 등에 대한 정보
- Accounting Information: 프로세스 실행에 사용된 CPU 사용량, 실행 유저 정보
- I/O 상태 정보 : 프로세스에 할당된 I/O 디바이스 목록

![image](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/83461362/222e1b00-5b07-4390-9ac1-fe4ae8745355)
```
💡 프로세스 실행 → 프로세스 생성 → 프로세스 주소 공간 (코드, 데이터, 스택) 생성 → 이 프로세스의 메타데이터들이 PCB에 저장됨
```

### PCB는 어떻게 관리되나요 ? ❓

주기억장치(Memory)의 `프로세스 테이블` 에 저장된다.

LinkedList 연결리스트 방식으로 관리된다. 

PCB List Head에 PCB들이 생성될때마다 뒤에 붙음 ! 

연결리스트 특성 상 삽입 삭제가 용이하기 때문에, 프로세스가 생성되면 해당 PCB가 생성되고 프로세스가 완료되면 제거된다.

### 그렇다면 PCB가 필요한 이유는? ❓

프로세스가 여러개일 때, CPU는 프로세스의 상태에 따라 스케줄링하고 교체해야한다. 이 때, 앞으로 **다시 수행할 대기 중인 프로세스에 관한 저장 값을 PCB에 저장**해두는 것이다. 프로세스를 교체하는 과정에서 문맥 교환(Context Switching)이 발생한다.

## 💡 Context Switching (문맥 교환)

CPU가 이전 프로세스의 상태를 PCB에 저장하고, 실행할 프로세스의 정보를 PCB에서 읽어서 레지스터에 적재하는 과정을 말한다.

1. 인터럽트 발생
2. 실행중인 CPU 사용 허가시간을 초과
3. 입출력을 위해 대기

등 **프로세스 상태 변경 시 발생**하게 된다.

![image](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/83461362/141e9278-de71-4a57-a540-8e886f38f4d2)

idle: 유휴 상태, Executing: 실행 상태

### 💡 문맥 교환 시 문제점

자주 일어나면 `오버헤드(Overhead)` 비용이 발생하여 성능이 떨어진다.

실행할 프로세스의 정보를 PCB에서 가져오는 동안 CPU가 일을 하지 않음 → 성능 저하를 일으킴

### 💡 해결

- **다중 프로그래밍 수준을 낮추거나(time slice 주기를 길게) 스케줄러 알고리즘의 개선으로** 문맥 교환 발생 빈도 감소

<aside>
💡 멀티프로그래밍 수준(다중 프로그래밍 수준): CPU에서 **동시에 실행되는 작업의 개수**

</aside>

- **`스레드`를 이용**해 문맥 교환 부하 최소화 (스레드는 메모리 영역을 공유하여 메모리 주소 관련 처리를 수행할 필요 X)

**출처**
* https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Operating%20System/PCB%20%26%20Context%20Switcing.md
* https://github.com/devSquad-study/2023-CS-Study/blob/main/OS/os_pcb_and_context_switching.md
