# TCP 3 way handshake & 4 way handshake

## 3 way handshake - 연결 성립

→ 장치들 사이에서 논리적인 접속을 성립(establish)하기 위해 TCP에서 사용하는 방법

즉, 정확한 데이터 전송을 보장하기 위해 상대방 컴퓨터와 사전에 세션을 수립하는 과정

### 방법

![Untitled](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/4fe69265-eec1-44ac-bf1f-f8a801e54966)


![Untitled 1](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/cad43fe9-defb-4777-aecc-bd2fd55b73e7)


1. Clinet → Server : TCP SYN
    1. 클라이언트는 서버에 접속을 요청하는SYN 패킷을 보냄. 이 때, 클라이언트는 SYN을 보낵 SYN/ACK 응답을 기다리는 SYN_SENT상태가 된다.
2. Server → Client : TCP SYN ACK
    1. 서버는 SYN요청을 받고 클라이언트에게 요청을 수락한다는 ACK와 SYN flag가 설정된 패킷을 발송하고, A가 다시 ACK으로 응답하기를 기다린다. 이 때, B서버는 SYN_RECEIVED상태가 된다.
3. Client → Server : TCP ACK
    1. 클라이언트는 B서버에게 ACK를 보내고 이후로부터는 연결이 성립되고, 데이터 송수신이 이루어진다. 이 때, 서버의 상태는 ESTABLISHED이다.

<aside>
💡 SYN : Synchronize sequence numbers
ANC : Acknowledgement

</aside>

---

### 4 way handshake - 연결 해제

→ 연결 성립 후 모든 통신이 끝났다면 연결을 해제하는 과정도 필요하다. 이게 4 way handshake이다.

### 방법

![Untitled 2](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/f75fccdf-747a-4019-950d-21ea50d06a39)


![Untitled 3](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/dc8d76d3-c913-4276-97fd-2dd5188b8c1c)



1. Client → Server : TCP FIN
    1. 클라이언트가 서버에 연결을 종료하겠다는 FIN flag를 전송한다.
2. Server → Client : TCP ACK
    1. 서버는 클라이언트에 확인메세지를 보내고, 자신의 통신이 끝날 때까지 기다린다. 이 때의 상태는 TIME_WAIT이다.
3. Server → Client : TCP FIN
    1. 서버가 통신이 끝났으면 연결이 종료되었다고 클라이언트에게 FIN flag를 전송한다.
4. Client → Server : TCP ACK
    1. 클라이언트는 확인했다는 메세지를 보내고 통신을 종료한다.

<aside>
💡 <참고 자료>
[https://mindnet.tistory.com/entry/네트워크-쉽게-이해하기-22편-TCP-3-WayHandshake-4-WayHandshake](https://mindnet.tistory.com/entry/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-%EC%89%BD%EA%B2%8C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-22%ED%8E%B8-TCP-3-WayHandshake-4-WayHandshake)

</aside>
