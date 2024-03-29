# OSI 모형

- Open Systems Interconnection Reference Model
  - 개방형 시스템 상호연결 참조 모델
- 국제 표준화 기구(ISO)에서 개발한 통신에 관한 계층화 표준 모델
- 컴퓨터 네트워크 프로토콜 디자인과 통신을 계층으로 나누어 개념적으로 설명한 것이다.

### 목적

- 분산된 이기종 시스템간의 네트워크 상호호환을 위한 표준 아키텍처를 정의할수 있다.
- 통신에 관련된 목적을 달성하기 계층별로 분할하여 분업이 가능하다. (Divide and conquer)
- 각 계층은 하위 계층의 기능만을 이용하고, 상위 계층에게 기능을 제공한다.

## 7계층

### L1 물리 계층 (Physical Layer)

| 전송단위 | 비트(Bit)                                                              |
| :-: | :-: |
| 프로토콜 | 모뎀, RS-232, 이더넷, USB 등 케이블, 블루투스, WIFI, LTE, 5G 등 안테나 |
| 장비     | 허브, 리피터, 네트워크 카드(NIC)                                       |

- 물리적인 장치의 전기적, 전자적 연결에 대한 명세
- 디지털 데이터를 아날로그적인 전기적 신호로 변환하여 물리적인 전송이 가능케 한다.
- 주소 개념이 없으며 물리적으로 연결된 노드간에 신호를 주고 받는다.
- 디지털 비트를 전기/무선/광 신호로 변환 하는 기능을 담당한다.

### L2 데이터링크 계층 (Data Link Layer)

| 전송단위 | 프레임(Frame)                                                                        |
| :-: | :-: |
| 프로토콜 | CSMA/CD, CSMA/CA, Slott Aloha, DAC/ADC, Multiplexer, Demultiplexer, MAC 주소 관리 등 |
| 장비     | L2 Switch, 모뎀, 기지국, AP                                                          |

- 인접한 노드간의 신뢰성 있는 데이터(프레임) 전송을 제어(Node-to-Node Delivery)
- 네트워크 카드의 MAC(Media Access Control)주소를 통해 목적지를 찾아간다.
- 물리 계층을 통해 전달 받은 정보의 신뢰성을 확인을 위해 흐름제어(Flow Control), 오류제어(Error Control), 회선제어(Line Control)을 수행한다.
- 논리링크제어계층, 매체접근제어계층이라는 두 개의 부계층으로 나뉜다.

### L3 네트워크 계층 (Network Layer)

| 전송단위 | 패킷(Packet)                                                |
| :-: | :-: |
| 프로토콜 | IP, ARP, ICMP, IGMP, RIP, RIP v2, OSPF, IGRP, EIGRP, BGP 등 |
| 장비     | 라우터, L3 Switch                                           |

- 종단간 전송을 위한 경로 설정을 담당한다. (End-To-End 혹은 Host-To-Host Delivery)
- 호스트로 도달하기 위한 최적의 경로를 라우팅 알고리즘을 통해 선택하고 제어한다.
- 종단간 전송을 위한 주소로 IP주소를 사용한다.
- 최대 크기 1500바이트
- 전송계층에서 전달 받은 정보를 적당한 크기로 쪼개고 각각에 헤더를 추가해 패킷을 생성한다.
  - 각각의 헤더는 논리주소를 포함

### L4 전송 계층 (Transport Layer)

| 전송단위 | 세그먼트(Segment) |
| :-: | :-: |
| 프로토콜 | TCP, UDP          |
| 장비     | L4 Switch         |

- 종단간 신뢰성 있는 데이터 전송을 담당한다. (End-To-End Reliable Delivery)
- 종단(Host)의 구체적인 목적지(Process)까지 데이터가 도달할 수 있도록 한다. (Process-To-Process Communication)
- Process를 특정하기 위한 주소로 Port Number를 이용한다.
- 신뢰성 있는 데이터 전송을 위해 분할과 재조합, 연결제어, 흐름제어, 오류제어, 혼잡제어를 수행한다.

### L5 세션 계층 (Session Layer)

| 전송단위 | 데이터(Data) 또는 메세지(Message) |
| :-: | :-: |

- 응용 프로그램간의 논리적인 연결(세션) 생성 및 제어를 담당한다.
- TCP/IP 통신 연결을 수립/유지/중단

### L6 표현 계층 (Presentation Layer)

| 전송단위 | 데이터(Data) |
| :-: | :-: |
| 프로토콜 | png, jpg 등  |

- 데이터 표현방식, 상이한 부호체계 간의 변화에 대해 규정한다.
- 송수긴간의 인코딩/디코딩, 압축/해제, 암호화/복호화 등의 역할을 수행한다.

### L7 응용 계층 (Application Layer)

| 전송단위 | 데이터(Data)               |
| :-: | :-: |
| 프로토콜 | TELNET, FTP, SMTP, HTTP 등 |

- 응용 프로그램의 정보를 활용하고 통신을 제어한다.
- 사용자와 직접 상호작용하는 계층이다.
- 응용서비스 HTTP, SMTP
