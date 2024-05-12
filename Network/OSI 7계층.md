# OSI 7 계층

## OSI 7 계층

![Untitled](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/2c76b7bb-03f7-4efb-b5ec-1ad4d75ac528)


### OSI 7 계층이란?

네트워크에서 통신이 일어난 과정을 7단계로 나눈 것

### 왜 나눴을까??

- 통신이 일어나는 과정을 단계별로 파악할 수 있도록 하기 위해서
- 7단계 중 특정한 곳에 이상이 생기면 해당 단계에서만으로도 문제를 해결 할 수 있기 때문에

---

### 1계층 - 물리계층(Physical Layer)

- 리피터, 케이블, 허브 등… 데이터를 전기적인 신호로 변환해서 주고받는 기능을 담당
- 신호 규칙에 의해 1과 0이 구별될 수 있어야 함

![Untitled 1](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/9d3fb9c6-bbe9-41bc-b327-adbd3b429264)


---

### 2계층 - 데이터 링크계층(DataLink Layer)

- 브릿지, 스위치 등… MAC주소를 사용하여 통신하는 계층
- 물리계층을 통해 송수신되는 정보의 오류와 흐름을 관리
- 안전한 정보 전달을 수행할 수 있도록 돕는 역할
- 이 계층에서 전송되는 단위 → 프레임(Frame)

![Untitled 2](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/1e8f581d-0fe8-4bda-b32c-2bd3f32e17d9)


---

### 3계층 - 네트워크 계층(Network Layer)

- 서로 다른 두 네트워크 간의 데이터 전송을 용이하게 하는 계층
- 두 네트워크가 동일한 네트워크에 있는 경우 필요 X
- 전송 계층의 세그먼트 ↔ 네트워크 계층의 패킷 (세그먼트 > 패킷)
- 데이터가 표적에 도달하기 위한 최상의 물리적 경로 찾기 → 라우팅
- 라우터를 통해 이동할 경로를 선택 (IP주소 지정)
- 라우팅, 흐름 제어, 오류 제어, 세그먼테이션 등… 수행
- 프로토콜 종류 : IP, ICMP, IGMP, IPsec 등…

![Untitled 3](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/dbbb983c-92bd-4dba-a6ff-b63ab0ceb229)


---

### 4계층 - 전송 계층(Transport Layer)

- TCP와 UDP프로토콜을 통해 통신을 활성화
- 포트 개방 및 프로그램 전송 기능 제공
- TCP : 신뢰성, 연결 지향적 → 데이터 전달
- UDP : 비신뢰성, 비연결성, 실시간 → 스트리밍

![Untitled 4](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/dd340117-6225-46c8-817c-2dba43ee8c57)


---

### 5계층 - 세션 계층(Session Layer)

- 두 기기 사이의 통신의 시작과 종료를 담당
- 세션(Session) : 통신이 시작될 때부터 종료될 때까지의 시간
- 세션의 개방과 폐쇄를 리소스가 낭비되지 않게 관리
- 데이터 전송을 체크포인트와 동기화
- 데이터가 통신하기 위한 논리적 연결을 담당
- TCP/IP 세션을 만들고 없애는 기능을 담당
    
![Untitled 5](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/0c67aead-96e5-4790-9287-139f6bae9e9d)

    

<aside>
💡 체크포인트 : 데이터를 끊어서 여러 단위로 보내는 것
(ex. 100MB의 데이터가 있다고 하면, 5MB씩 끊어서 보내는데, 3번째 5MB에서 문제가 발생하면 해당 체크포인트부터 다시 전송하면 된다. 체크포인트가 없다면 처음부터 전체 데이터를 다시 보내야 한다.)

</aside>

---

### 6계층 - 프레젠테이션 계층(Presentation Layer)

- 데이터를 준비하는 역할
- 애플리케이션이 소비할 수 있도록 데이터를 프레젠테이션
- 데이터의 변환, 암호화, 압축
- 각 통신 장치마다 인코딩하는 방법이 다를 수 있으므로, 이해할 수 있는 구문으로 데이터를 변환

![Untitled 6](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/40891b65-0835-40cb-a83b-8a3755f8477e)


### 7계층 - 응용 프로그램 계층(Application Layer)

- 사용자의 데이터와 직접 상호작용하는 유일한 계층
- 클라이언트가 소프트웨어 어플리케이션을 통해 통신을 개시하기 위해 해당 계층에 의지
- 포로토콜, 데이터를 조작하는 역할
- 프로토콜 : HTTP, SMTP(이메일 통신)

![Untitled 7](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/a2f65ed9-fa58-4069-9855-ddf45910596f)


<aside>
💡 <참고자료>
[https://www.cloudflare.com/ko-kr/learning/ddos/glossary/open-systems-interconnection-model-osi/](https://www.cloudflare.com/ko-kr/learning/ddos/glossary/open-systems-interconnection-model-osi/)

</aside>
