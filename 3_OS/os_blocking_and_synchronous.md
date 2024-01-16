# Blocking/Non-Blocking & Synchronous/Asynchronous

## 1. Blocking

### 개념

- 직접 제어할 수 없는 대상의 작업이 끝날 때까지 기다려야 하는 경우
- ex) 호출하는 함수가 I/O 작업을 요청할 때 I/O 처리가 완료될 때까지 아무 일도 하지 못하고 기다리는 것

![blocking](https://github.com/Network-Leader/2023-Winter-CS-Study/assets/49124725/b605caf1-b184-4aba-a649-430887ceca4c)

- 개발 부서 전체 작업의 제어권을 가진 팀장이 엔지니어 A에게 넘겨주게 된다.
- 엔지니어 A가 작업을 수행할 동안 개발 부서 전체는 이를 기다리게 된다.
- 엔지니어 A가 작업을 마치고 팀장에게 알리면서 동시에 제어권도 돌려준다.  
-> 제어권이 없는 상태에서는 Blocking이 되며 다른 일을 할 수 없는 상태가 된다.  
   <br/>

## 2. Non-Blocking

### 개념

- 직접 제어할 수 없는 대상의 작업이 완료되기 전에 제어권을 넘겨주는 경우
- 직접 제어할 수 없는 대상의 작업처리 여부와 상관 없음
- ex) 호출하는 함수가 I/O 작업을 요청한 뒤 I/O 작업에 대한 처리 완료 여부와 상관없이 바로 자신의 작업을 수행할 수 있는 것

![non-blocking](https://github.com/Network-Leader/2023-Winter-CS-Study/assets/49124725/7fa046da-db63-452d-afdd-c5dc0cb1ca47)

- 제어권을 바로 팀장에게 돌려주기 때문에 개발 부서는 엔지니어 A의 작업을 기다리지 않는다.  
  -> 다른 일을 할 수 있는 상태가 된다.  
   <br/>

## 3. Synchronous

### 개념

- 두 가지 이상의 대상 (함수, 애플리케이션 등)이 서로 시간을 맞춰 행동하는 것
- 메소드를 실행시킴과 동시에 반환 값이 기대되는 경우
- ex) 호출한 함수가 호출된 함수의 작업이 끝나 결과를 반환하기를 기다리거나, 지속적으로 호출된 함수에게 확인을 요청하는 경우

![sync1](https://github.com/Network-Leader/2023-Winter-CS-Study/assets/49124725/445bc53d-d700-42c5-9dd1-21dabbdc962a)

- A가 끝나는 시간과 B가 시작하는 시간을 맞추는 것

![sync2](https://github.com/Network-Leader/2023-Winter-CS-Study/assets/49124725/67ec660b-c7c5-44db-a57e-70cbe5209859)

- A와 B가 시작 시간 또는 종료 시간이 일치하는 것
- ex) A, B 스레드가 동시에 작업을 시작하는 경우, 메소드 리턴 시점 (A)과 결과를 전달받는 시점(B)이 일치하는 경우
  <br/>

## 4. Asynchronous

### 개념

- 작업을 수행하는 주체의 시작시간과 끝나는 시간에 관계없이 각자 별도의 시작 시간, 끝나는 시간을 가지고 있을 경우
- 두 가지 이상의 대상이 서로 시간을 맞춰 행동하지 않는 것

![async](https://github.com/Network-Leader/2023-Winter-CS-Study/assets/49124725/0ad573a5-6916-4806-9fb8-775aecfc9a35)

- 제어권을 바로 팀장에게 돌려주기 때문에 개발 부서는 엔지니어 A의 작업을 기다리지 않는다.  
  -> 다른 일을 할 수 있는 상태가 된다.  
   <br/>

## 5. Blocking vs Synchronous & Non-Blocking vs Asynchronous

- Blocking: 작업이 끝나기를 기다리다가 끝나면 다음 작업을 수행하는 것
- Synchronous: 두 가지 이상의 작업이 서로 시간을 맞춰 행동하는 것
- Non-Blocking: 다른 작업이 끝날 때까지 기다리지 않는 것
- Asynchronous: 두 가지 이상의 작업이 서로 시간을 맞춰 행동하지 않는 것  
  <br/>

## 6. Blocking/Non-Blocking & Synchronous/Asynchronous 조합

### Synchronous Blocking I/O

![sync_block](https://github.com/Network-Leader/2023-Winter-CS-Study/assets/49124725/a94acfdc-a2a7-44fc-b24c-4fcd68b3a4ae)

- Synchoronous: Application의 Read() 메소드가 리턴하는 시간과 Kernel에서 read I/O작업 결과가 반환되는 시간이 일치한다.
- Blocking: Application은 Kernel에게 read I/O 작업 요청을 하면서 동시에 제어권을 넘긴다. Application은 Kernel의 I/O 작업이 완료될 때까지 다음 작업을 수행하지 못하고 대기한다.

### Synchronous Non-Blocking I/O

![sync_nonblock](https://github.com/Network-Leader/2023-Winter-CS-Study/assets/49124725/d4052492-01c8-4597-ae31-15c02d2b48a1)

- Synchoronous: Application의 Read() 메소드가 리턴하는 시간과 Kernel에서 read I/O작업 결과가 반환되는 시간이 일치한다.
- Non-Blocking: Application은 Kernel에게 read I/O 작업 요청과 동시에 제어권을 넘기지만, Kernel의 작업 완료 여부와 관계없이 Application에게 제어권이 다시 반환된다. Kernel의 I/O 작업이 완료되면 그 결과를 Application에게 반환한다.

### Asynchronous Blocking I/O

![async_block](https://github.com/Network-Leader/2023-Winter-CS-Study/assets/49124725/4e01cd02-57d2-4152-b2f7-89fcf1766fac)

- Asynchronous: Application의 Read() 메소드가 리턴하는 시간과 Kernel에서 read I/O작업 결과가 반환되는 시간이 일치하지 않는다.
- Blocking: Application은 Kernel에게 read I/O 작업 요청을 하면서 동시에 제어권을 넘긴다. Application은 Kernel의 I/O 작업이 완료될 때까지 다음 작업을 수행하지 못하고 대기한다.

### Asynchronous Non-Blocking I/O

![async_nonblock](https://github.com/Network-Leader/2023-Winter-CS-Study/assets/49124725/ffbead1c-121f-4bdd-bc2b-08e162589605)

- Asynchronous: Application의 Read() 메소드가 리턴하는 시간과 Kernel에서 read I/O작업 결과가 반환되는 시간이 일치하지 않는다.
- Non-Blocking: Application은 Kernel에게 read I/O 작업 요청과 동시에 제어권을 넘기지만, Kernel의 작업 완료 여부와 관계없이 Application에게 제어권이 다시 반환된다. Kernel의 I/O 작업이 완료되면 그 결과를 Application에게 반환한다. Application은 콜백함수를 통해 그 결과를 처리한다.
<br/>
  
## 참고자료

https://velog.io/@guswns3371/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-Synchronous%EC%99%80-Asynchronous-Blocking%EA%B3%BC-Non-Blocking  
https://velog.io/@jaewan/CSPython%EB%8F%99%EA%B8%B0%EB%B9%84%EB%8F%99%EA%B8%B0%EC%99%80-%EB%B8%94%EB%A1%9D%EB%85%BC%EB%B8%94%EB%A1%9D-SynchronousAsynchronous-BlockingNonblocking
