# TCP(흐름제어/혼잡제어)

## TCP란?

- 전송 제어 프로토콜(Transmission Control Protocol, TCP)
- 전송계층에 위치
- 네트워크 통신에서 신뢰적인 연결 방식
- 신뢰할 수 없는 네트워크(Unreliable network)에서 신뢰할 수 있는 네트워크(Reliable network)를 보장할 수 있도록 하는 프로토콜
- 혼잡 방지 알고리즘(Network congestion avoidance algorithm)을 사용

<aside>
💡 신뢰할 수 있는 네트워크(Reliable network)를 보장한다는 것 → 아래 4개의 문제를 해결
1. 손실 : 패킷이 손실될 수 있다.
2. 순서: 패킷의 순서가 바뀔 수 있다.
3. 혼잡 : 네트워크가 혼잡하다.
4. 과부하 : 수신자(Receiver)가 과부하될 수 있다.

</aside>

→ TCP는 위 4가지 문제를 “흐름 제어”와 “혼잡 제어” 2 가지 기법으로 해결한다.

---

## (Optional) 전송의 과정

1. 너무 내용이 많아서 추가로 작성 예정

---

## 흐름 제어(Flow Control)

### 데이터 전송 과정에서 문제가 생기는 이유

- 수신 측(Receiver)이 송신 측(Sender)보다 데이터 처리속도가 느릴 경우 발생하는 문제점을 해결하기 위한 방식
- Receiver가 Sender보다 느릴 경우 Receiver Buffer(또는 TCP Buffer)라는 임시 저장소에 저장하게 되는데, 이 버퍼의 용량을 넘게 되면 문제가 발생 → 버퍼의 용량을 넘치지 않게 잘 조절해야 함
- Receiver는 버퍼의 용량을 관리하기 위해 Sender에게 용량이 얼마나 남았는지를 알려줌. 이 때, 이 것을 “수신 윈도우(Receive Window)”라고 함.
- 버퍼의 용량을 초과 → 데이터 손실 → 문제 발생

### 흐름 제어란?

- 위에서 나온 데이터 전송 과정에서 생기는 (버퍼가 넘쳐 데이터가 손실되는) 문제점을 해결하기 위한 방법(흐름 제어를 하기 위해 여러 기법들이 존재) → Sender와 Receiver 사이의 문제
    1. Stop and Wait : 매번 전송한 패킷에 대해 확인 응답(ACK)을 받으면 패킷을 전송하는 기법
        
        ![Untitled](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/fcdbb63e-1a65-42fe-b8d2-6738530ea85d)
        
  문제점
  
  - 패킷을 매 번 하나씩 보내야하기 때문에 매우 비효율적
      
      2. Sliding window : Receiver가 설정한 Receive Window의 크기만큼 Sender가 패킷을 전송할 수 있게 하여 데이터의 흐름을 “동적”으로 조절하는 제어 기법
          
          ![Untitled 1](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/235e9e0e-bc31-4a91-8342-573a026010a9)

          ![Untitled 2](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/70a830a5-8ec1-4bae-8aa4-1adf9b8ba06b)
          
          → Stop and Wait 기법의 비효율성을 개선한 기법.
          
          1. 즉, TCP통신을 하면 Receiver → Sender 방향으로 확인 응답(ACK)을 보낼 때, TCP 헤더에 Receive Window의 크기를 같이 넣어서 보냄.
          2. 그러면 Sender는 다음 전송 때, Receiver가 받을 수 있는 크기만큼만 보냄
          3. 해당 과정을 데이터가 모두 전송될 때 까지 반복

---

## 혼잡 제어(Congestion Control)

- 네트워크가 혼잡할 경우 데이터 손실 또는 오버플로우 등의 문제를 줄이기 위해 Sender의 데이터 전송 속도를 강제로 줄이게 되는데 이것이 바로 혼잡 제어
- 흐름제어가 Sender ↔ Receiver의 사이에서 이루어졌다면, 혼잡 제어는 Host ↔ Router를 포함한 더 넓은 관점(네트워크)에서의 전송 문제를 다룬다.
    1. AIMD(Additive Increase / Multiplicative Decrease) : 패킷을 하나씩 보내면서 Window의 크기를 1씩 증가시켜가며 전송.
        
        
        ![Untitled 3](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/f148b00a-8a4d-41b1-ab6c-71ac89b7bafe)


        
        1. Window의 크기(한 번에 보낼 수 있는 패킷의 양)를 1씩 증가시키면서 전송
        2. 패킷 전송 실패 or 일정 시간이 넘으면 Window의 크기를 절반으로 감소
        
        → 이 방식을 통하면 시간이 흐르면 대부분의 호스트들이 네트워크를 공평하게 사용할 수 있음(평형상태로 수렴)
        
        <문제점>
        
        - (네트워크에 늦게 진입한다면) 초기에 네크워크의 높은 대역폭을 사용할 수 없음
        - 네트워크가 혼잡해지는 상황을 미리 감지할 수 없음 → 혼잡해지고 나서야 대역폭을 줄이는 방식
    
    1. Slow Start(느린 시작) : AIMD와 비슷하지만, AIMD의 선형적인 증가와는 다르게 1, 2, 4, 8, …과 같이 지수적으로 증가시키는 방식(ACK이 잘 도착한다면 Window를 1씩 증가시켜 전송하는 방식)
        
        ![Untitled 4](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/f6f0ccbf-d9ab-44ec-9459-a58ad8b2bb9a)
        
        1. 패킷을 하나씩 보내며, ACK이 잘 도착한다면 ACK마다 패킷을 1씩 증가시키며 전송
            
            (즉, 한 전송 주기가 끝나면 Window의 크기는 2배가 된다)
            
        2. 혼잡 현상 발생 시 절반으로 줄이는 AIMD와는 다르게 Window 사이즈를 1로 줄여버린다.
    
    1. 혼잡 회피(Congestion Avoidance) : 혼잡이 감지되면 지수적이 아닌 가산적인 증가 방식을 채택하는 기법
    2. 빠른 재전송(Fast Retrasmit) : 정상적인 재전송 큐 과정을 따르지 않고, 중간에 누락된 세그먼트만 빠르게 재전송하는 방식
    3. 빠른 회복(Fast Recovery) : 혼잡이 감지되면 window의 크기를 1로 줄이지 않고 반으로 줄이고 선형(AIMD)으로 증가시키는 방식.
