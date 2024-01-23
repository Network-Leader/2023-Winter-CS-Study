### ****웹 통신의 큰 흐름: https://www.google.com 을 접속할 때 일어나는 일****
<details>
<summary>접기/펼치기</summary>
<div markdown="1">

1. Host가 google.com을 검색하면 OS에서 NIC(network Interface Card, 이거 하나 당 IP하나씩 받을 수 있음)를 통해 요청을 보내야 한다. Host는 google의 IP주소를 알아야 한다.
2. 내가 IP주소를 아는지 모르는지 판단하기 위해 hosts와 DNS cache에서 mapping 정보를 확인한다. (DNS Lookup)
3. 2)에서 없으면 DNS서버로 요청을 보내서 응답을 받는다. (공유기 / 라우터가 DNS를 알고있음. 인터넷 망을 통해 DNS서버로 요청을 한다.)
4. 그 IP주소로 http request를 보내고 응답을 받는다. (해당 IP로 가는 경로는 중간중간의 Router들의 Routing Table에 저장되어있다.)

</div>
</details>

### ****DNS 서버에 대해 설명해주세요****
<details>
<summary>접기/펼치기</summary>
<div markdown="1">

DNS서버란 도메인 이름을 IP주소로 바꿔주는 역할을 하는 서버입니다. 이로 인해 클라이언트는 IP주소를 기억하지 않고 해당 주소의 웹사이트에 접근할 수 있습니다.

도메인(Domain) : 웹사이트의 위치 (ex, 도메인 이름 google.com은 IP주소 142.250.196.142를 의미)

도메인과 URL의 차이점 : 웹주소인 URL에는 도메인 이름과 전송 프로토콜 및 경로 등의 정보가 포함되어 있습니다.

![Network_DNSanswer.png](img%2FNetwork_DNSanswer.png)

- **Root 네임 서버** : DNS 레코드를 요청하는 첫 단계입니다. 비영리 단체인 ICANN(Internet Corporation for Assigned Names and Numbers)이 관리합니다.
- **TLD(최상위 도메인) 네임 서버** : TLD 네임서버는 .com, .co.kr 과 같은 점 뒤에오는 도메인 확장자를 사용하는 모든 도메인 정보를 유지합니다.
- **Authoritative 네임 서버** : 실제 도메인의 IP주소가 기록되는 서버입니다. 도메인/호스팅 업체의 '네임서버'를 말합니다.
- **Recursive(재귀) 네임 서버** : 인터넷 사용자가 가장 먼저 접근하는 DNS 서버로 특정 도메인에 대한 IP정보를 캐시 형태로 저장해놓습니다. 대표적으로 KT/LG/SK 와 같은 ISP(통신사) DNS 서버가 있습니다

</div>
</details>

### URL

HTTP 통신 흐름은 'URL이 입력되었을 때 일어나는 과정'을 의미

URL은 특정 리소스에 대한 구체적인 위치를 의미하며, 보통 'https://www.google.com'처럼 나타낸다. URL을 주소창에 입력하면, 리소스 요청이 시작된다.

### IP 주소

컴퓨터 네트워크에서 장치들이 서로를 인식하고 통신을 하기 위해서 사용하는 특수한 번호

### Domain Name

IP 주소를 문자로 표현한 주소

## 웹(HTTP) 통신의 흐름

![Network_web-communication.png](img%2FNetwork_web-communication.png)

1. **사용자가 웹브라우저 검색창에 www.google.com 입력**
2. **웹브라우저는 해당 도메인 주소와 상응하는 IP 주소를 찾기 위해  캐싱된 DNS 기록을 확인**
    1. 이때, 브라우저는 DNS 기록을 찾기 위해 browser → OS → router → ISP 순으로 확인
    2. 이 단계에서 캐싱된 기록에 없을 경우, 다음단계로 넘어감
3. **만약 캐시가 없다면 ISP의 DNS 서버는 IP주소를 찾기 위해 DNS query를 시작**
    1. DNS 쿼리는 IP주소를 찾을 때까지 반복(**recursive search**)
4. **DNS가 웹브라우저에게 찾는 사이트의 IP주소를 응답**
5. **IP 주소를 받으면 일반적으로 TCP 통신을 시작**
    - TCP 연결은 three-way handshake 방식
6. **HTTP 프로토콜로 요청**
    - TCP로 연결이 되면, 브라우저는 GET요청을 통해 서버에게 www.google.com의 웹페이지를 요구
7. **웹 어플리케이션 서버(WAS)와 데이터베이스에서 우선 웹페이지 작업 처리**
    - 웹 서버 혼자서 모든 로직 처리 및 데이터 관리를 하게되면 서버에 과부하가 일어날 가능성이 높다. 그렇기에 서버의 일을 돕는 조력자 역할을 하는 것이 WASㅇ

   > 웹서버 : 정적인 컨텐츠(HTML, CSS, IMAGE 등)를 요청받아 처리하여 제공하는 서버
   >

   > WAS : 동적인 컨텐츠(JSP, ASP, PHP 등)를 요청받아 처리하여 제공하는 서버 => 주로 DB서버와 함께 사용
   >

   ![Network_WAS.png](img%2FNetwork_WAS.png)

8. **WAS에서의 작업 처리 결과들을 웹 서버로 전송**
9. **웹서버는 웹브라우저에게 html 문서 결과를 응답**

   응답 status code로 서버 요청에 따른 상태를 보냄

    - 1xx ▶️ 정보만 담긴 메세지
    - 2xx ▶️ response 성공
    - 3xx ▶️ 클라이언트를 다른 URL로 리다이렉트
    - 4xx ▶️ 클라이언트 측에서 에러 발생
    - 5xx ▶️ 서버 측에서 에러 발생
10. **웹브라우저는 html 컨텐츠를 표시**

## DNS 서버

### DNS

DNS는 도메인 이름과 IP 주소를 저장하고 있는 분산 데이터베이스로, **웹사이트를 위한 주소록**

숫자로 된 IP 주소(ex. 63.245.217.105) 대신 사용자가 사용하기 편리하도록 주소를 매핑해주는 역할

### **분산 계층 데이터베이스**

만약에 DNS 한 곳에 모든 질의를 한다면 간단하다. 하지만 중앙 집중 데이터베이스는 서버의 고장, 트래픽양, 먼 거리의 중앙 집중 데이터베이스, 유지관리 등의 문제를 고려하여 확장성이 없음

그래서 DNS는 많은 서버를 이용해 **계층 형태로 분산**

![Network_DNS.png](img%2FNetwork_DNS.png)

- **루트 DNS 서버**

  1000개 이상의 루트 서버 인스턴스가 전세계에 흩어져 있다.

  루트 네임 서버는 TLD 서버의 IP 주소들을 제공

- **최상위 레벨 도메인 네임 (top-level domain, TLD) DNS 서버**

  com, org, net, edu, gov와 같은 상위 레벨 도메인과 kr, uk, fr와 같은 모든 국가의 상위 레벨 도메인에 대한 TLD 서버

  TLD 서버는 책임 DNS 서버에 대한 IP 주소를 제공

- **책임 (authoritative) DNS 서버**

  조직의 자체 DNS 서버, 조직의 명명 된 호스트에 대한 IP 매핑에 권한있는 호스트 이름을 제공


### DHCP

- Dynamic Host Configuration Protocol

![Network_DHCP.png](img%2FNetwork_DHCP.png)

- 호스트의 IP 주소와 TCP/IP 설정을 클라이언트에 의해 자동으로 제공하는 응용 계층 프로토콜

  → 사용자는 DHCP 서버에서 자신의 IP 주소, 가장 가까운 라우터의 IP 주소, 가장 가까운 **DNS 서버의 주소**를 받는다.


### ARP

- Address Resolution Protocol
- 네트워크상에서 IP 주소를 물리적 네트워크 주소로 바인딩시키기 위해 사용하는 프로토콜
- DHCP로 얻은 라우터의 IP 주소를 MAC 주소로 변환

## DNS 서버의 주소 찾기

### **DNS query**

ISP(Internet Service Provider)의 DNS서버(**DNS recursor**)가 호스팅하고 있는 서버의 IP주소를 찾기 위해 DNS query를 보냄

- **DNS query의 목적**
    - DNS 서버들을 검색해서 해당 사이트의 IP주소 찾기
    - IP주소를 찾을 때까지 DNS서버에서 다른 DNS서버를 오가며 에러가 날때까지 반복적으로 검색
    - **재귀적 질의(recursive search), 반복적 질의(iterative query)**

![Network_DNSquery.png](img%2FNetwork_DNSquery.png)

1. DNS 서버에 DNS Query(www.example.com)를 전송

   → 우리나라의 경우에는 통신사별로 지정된 DNS 서버가 존재

2. DNS 서버는 **루트 네임 서버**에 DNS Query를 질의

   → 루트 네임 서버는 **.com의 ip주소**를 반환

3. .com 네임 서버에 DNS 쿼리를 질의

   → .com 네임 서버는 **example.com의 ip주소**를 반환

4. [example.com](http://example.com/) 네임 서버에 DNS 쿼리를 질의

   → www.example.com의 IP 주소를 반환


![Network_domain-levels.png](img%2FNetwork_domain-levels.png)

DNS 서버는 계층화 구조를 이루는데, 최상단 계층인 가장 뒷쪽(.com, .kr 등등)을 담당하는 DNS 서버는 전세계에 13개만 존재

요청한 호스트에게 매핑 결과를 전달하기 위해 많은 질의 메세지가 필요

→ 질의 전송을 줄이기 위해서 **DNS 캐싱** 방법을 사용

### **DNS 캐싱**

DNS 지역 성능 향상과 네트워크의 DNS 메세지 수를 줄이기 위해서 캐싱을 사용

- DNS 서버가 DNS 응답을 받았을 때 그것을 로컬 메모리에 응답 정보를 저장
- 호스트 이름과 IP 주소 쌍이 DNS 서버에 저장되면 처음 브라우저가 캐싱된 DNS를 확인하고 캐싱된 기록이 없을 때 DNS 질의로 넘어간다.
- 호스트 이름과 IP 주소 사이 매핑과 호스트는 영구적이지 않기 때문에 특정 기간마다 저장된 정보를 제거

### 참고자료

[웹 통신의 큰 흐름](https://carnival.tistory.com/53)

[[네트워크] 웹 통신의 흐름](https://velog.io/@woo0_hooo/네트워크-웹-통신의-흐름)

[[Network] 웹 통신의 흐름](https://hello-judy-world.tistory.com/189)