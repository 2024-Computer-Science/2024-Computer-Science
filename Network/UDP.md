# UDP

## UDP

- User Datagram Protocol의 약자로 “데이터그램” 단위로 처리하는 프로토콜(전송 계층)
- 비디오 재생 or DNS 조회와 같이 시간에 민감한 전송을 위해 사용
- 데이터를 아주 빠르게 전송할 수 있지만, 전송 중에 패킷이 손실될 수도 있음

<aside>
💡 Datagram이란?
- IP계층의 가변길이 패킷
- 헤더와 데이터 부분으로 구성
- 헤더는 20Byte ~ 60Byte
- 라우팅(경로 지정)과 전달에 필요한 정보를 포함
- TCP/IP에서는 헤더를 4바이트 단위로 표시

</aside>

## 등장 배경

1. IP는 Host to Host만을 지원. 그러나 하나의 디바이스 안에서 많은 프로그램들이 통신할 경우 IP만으로는 감당 X → Port 등장
2. IP에서 오류가 발생한다면 ICMP에서 알려주긴 하지만, 대처할 수 없기 때문에 IP보다 상위 계층에서 처리를 해주어야 한다. → TCP & UDP 등장

<aside>
💡 ICMP란?
인터넷 제어 메세지 프로토콜 : 컴퓨터 상에서 돌아가는 운영체제에서 오류 메시지를 전송받는데 주로 사용됨

</aside>

## TCP & UDP이 위 문제를 해결하는 방법

- TCP : 데이터의 분실, 중복, 순서 변경을 자동으로 감지 및 보정 → 송수신 데이터의 안정성 보장
- UDP : IP가 제공하는 정도의 수준만을 제공해서 에러가 날 수도 있지만, 데이터를 신속하게 보낼 수 있다 → 송수신 데이터의 신속성 보장

## UDP를 주로 사용하는 곳

- 실시간 스트리밍
- VoIP(음성통화)
- 온라인 게임
- 실시간 동영상 서비스
- DNS(Domain Name System)
- 등…

→ 속도가 중요한 곳에 사용

## UDP Header

![Untitled](https://github.com/2024-Computer-Science/2024-Computer-Science/assets/21362256/8414059f-d5ab-48b6-b704-2e2a6fc6044e)

- Source Port : 시작 포트
- Destination Port : 도착지 포트
- Length : 길이
- Checksum : 오류 검출

→ 위와 같이 간단하기 때문에 TCP보다 가볍고 빠름. but 신뢰 낮음

즉, TCP → 연결성 / UDP → 비연결성 으로 정의 가능

<aside>
💡 <참고자료>
[https://www.cloudflare.com/ko-kr/learning/ddos/glossary/user-datagram-protocol-udp/](https://www.cloudflare.com/ko-kr/learning/ddos/glossary/user-datagram-protocol-udp/)

</aside>
