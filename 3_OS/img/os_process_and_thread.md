# 프로세스와 스레드

## 1. 프로세스

### 개념

- 운영체제로부터 자원을 할당받은 작업의 단위
- 컴퓨터에서 작업 중인 프로그램
- 하나의 프로세스는 반드시 하나 이상의 스레드를 가짐
<br/>

### 자원 구조

![process](https://github.com/Network-Leader/2023-Winter-CS-Study/assets/49124725/87ac2ea1-02ab-4d14-966d-f3ec4bdd13f7)

- 코드 영역(Code/Text): 프로그래머가 작성한 프로그램 함수들의 코드가 CPU가 해석 가능한 기계어 형태로 저장
- 데이터 영역(Data): 코드가 실행되면서 사용하는 전역 변수나 각종 데이터들의 모임
- 스택 영역(Stack): 지역 변수와 같은 호출한 함수가 종료되면 되돌아올 임시적인 자료를 저장하는 독립적인 공간, 스택은 함수의 호출과 동시에 할당되며 함수의 호출이 완료되면 소멸, 스택 영역 초과 시 스택오버플로우 발생
- 힙 영역(Heap): 생성자, 인스턴스와 같은 동적으로 할당되는 데이터들을 위해 존재하는 공간, 사용자에 의해 메모리 공간이 동적으로 할당되고 해제
<br/>

### 자원 공유

- 기본적으로 각 프로세스는 메모리에 별도의 주소 공간에서 실행되기 때문에 한 프로세스가 다른 프로세스의 변수나 자료 구조의 접근 불가
- IPC/LPC 등의 방법으로 공유 가능
- 다만, 프로세스의 자원 공유는 단순히 CPU 레지스터 교체 뿐만 아니라 RAM과 CPU 사이 캐시 메모리까지 초기화하기 때문에 자원 부담이 큼
<br/>

### 생명 주기

#### 스케줄링

운영체제에서 CPU를 사용할 수 있는 프로세스를 선택하고 CPU를 할당하는 작업 ex) FCFS, SJF, 우선순위, RR, Multi-level Queue 등
<br/>

#### 상태

![process_state](https://github.com/Network-Leader/2023-Winter-CS-Study/assets/49124725/90181efa-7d91-4559-8d67-4574921085e3)

- New: 프로세스가 생성되고 아직 준비되지 않은 상태
- Ready: 프로세스가 실행을 위해 기다리는 상태, CPU를 할당받을 수 있는 상태이며 언제든지 실행할 준비가 되어있음
- Running: 프로세스가 CPU를 할당받아 실행되는 상태
- Waiting: 프로세스가 특정 이벤트(입출력 요청 등)가 발생하여 대기하는 상태, CPU를 할당받지 못하며 이벤트가 발생하여 다시 상태로 전환될 때까지 대기
- Terminated: 프로세스가 실행을 완료하고 종료된 상태, 더는 실행될 수 없으며 메모리에서 제거
<br/>

#### 상태 전이

프로세스가 실행되는 동안 상태가 OS에 의해 변경되는 것

- Admitted (new → ready): 프로세스 생성을 승인 받음
- Dispatch (ready→ running): 준비 상태에 있는 여러 프로세스들 중 하나가 스케줄러에 의해 실행됨
- Interrupt (running → ready): Timeout, 예기치 않은 이벤트가 발생하여 현재 실행 중인 프로세스를 준비 상태로 전환하고, 해당 작업을 먼저 처리
- I/O or event wait (running → wainting): 실행 중인 프로세스가 입출력이나 이벤트를 처리해야 하는 경우, 입출력이나 이벤트가 끝날 때까지 대기 상태로 전환
- I/O or event completion (waiting → ready): 입출력이나 이벤트가 모두 끝난 프로세스를 다시 준비 상태로 만들어 스케줄러에 의해 선택될 수 있는 상태로 전환
<br/>

#### Context Switching

- CPU가 한 프로세스에서 다른 프로세스로 전환할 때 발생하는 일련의 과정
- 동작 중인 프로세스가 대기를 하면서 해당 프로세스의 상태(Context)를 보관하고, 대기하고 있던 다음 순서의 프로세스가 동작하면서 이전에 보관했던 프로세스의 상태를 복구
- Context Switching의 주체는 스케줄러
- PCB 저장 및 복원 비용, CPU 캐시 메모리 무효화에 따른 비용, 프로세스 스케줄링 비용 등의 이유로 오버헤드 발생 가능
<br/>

#### PCB(Process Control Block)

- 프로세스를 관리하기 위해 해당 프로세스의 상태 정보를 담고 있는 자료구조
- 프로세스가 생성되면 메모리의 해당 프로세스의 PCB가 함께 생성, 종료 시 삭제

![process_context_switching](https://github.com/Network-Leader/2023-Winter-CS-Study/assets/49124725/301e0aec-d11f-40f1-b3ee-846518ea0d26)

1. CPU는 Process P1을 실행한다 (Executing)
2. 일정 시간이 지나 Interrupt 또는 system call이 발생한다. (CPU는 idle 상태)
3. 현재 실행 중인 Process P1의 상태를 PCB1에 저장한다. (Save state into PCB1)
4. 다음으로 실행할 Process P2를 선택한다. (CPU 스케줄링)
5. Process P2의 상태를 PCB2에서 불러온다. (Reload state from PCB2)
6. CPU는 Process P2를 실행한다. (Executing)
7. 일정 시간이 지나  Interrupt 또는 system call이 발생한다. (CPU는 idle 상태)
8. 현재 실행 중인 Process P2의 상태를 PCB2에 저장한다. (Save state into PCB2)
9. 다시 Process P1을 실행할 차례가 된다. (CPU 스케줄링)
10. Process P1의 상태를 PCB1에서 불러온다. (Reload state from PCB1)
11. CPU는 Process P1을 중간 시점 부터 실행한다. (Executing)
<br/>
  
## 2. 스레드

### 개념

- 프로세스가 할당받은 자원을 이용하는 실행 흐름의 단위
<br/>

### 자원 공유

![thread](https://github.com/Network-Leader/2023-Winter-CS-Study/assets/49124725/09a5ec3e-ab9a-4fd2-b698-9bba3e4a378e)

- 스레드끼리 프로세스의 자원을 공유
- 스택만 할당받아 복사(각 스레드마다 독립적인 스택 가짐), 코드/데이터/힙은 프로세스 내 다른 스레드와 공유
- 자원의 생성과 관리의 중복성 최소화
<br/>

### 생명 주기

#### 스케줄링

운영체제에서 다중 스레드를 관리하며, CPU를 사용할 수 있는 스레드를 선택하고, CPU를 할당하는 작업, 하나의 프로세스 내에서 다수의 스레드가 동작하는 형태이기 때문에, 스레드 간의 상호작용과 동기화 문제를 고려해야 함 ex) RR, Multi-level Queue 등
<br/>

#### 상태

![thread_state](https://github.com/Network-Leader/2023-Winter-CS-Study/assets/49124725/8f8fb06a-2936-404f-a4cd-c549ae3920d4)

- New: 스레드가 생성되고 아직 호출되지 않은 상태
- Runnable: 스레드가 실행을 위해 기다리는 상태, CPU를 할당받을 수 있는 상태이며 언제든지 실행할 준비가 되어있음
- Blocked: 스레드가 특정 이벤트(입출력 요청 등)가 발생하여 대기하는 상태, CPU를 할당받지 못하며 이벤트가 발생하여 다시 runnable 상태로 전환될 때까지 대기
- Terminated: 스레드가 실행을 완료하고 종료된 상태, 더는 실행될 수 없으며 메모리에서 제거
<br/>

#### Context Switching

- 멀티 스레딩 환경에서 스레드 간의 실행을 전환
- 하나의 프로세스 내의 스레드를 교환
- 컨텍스트 스위칭의 주체는 스케줄러
- 프로세스 Context Switching보다 빠름(TCB는 스택 및 간단한 레지스터 포인터 정보만을 저장)
<br/>

#### TCB(Thread Control Block)

- 각 스레드마다 운영 체제에서 유지하는 스레드에 대한 정보를 담고 있는 자료구조
- PCB 안에 들어있음
- 스레드가 생성되면 메모리의 해당 스레드의 TCB가 함께 생성, 종료 시 삭제
- 뮤텍스나 세마포어 등 동기화 기법을 사용하거나 스레드 간 자원 공유할 때 사용
<br/>
  
### 멀티 프로세스 vs 멀티 스레드

#### 멀티 프로세스

- 하나의 프로그램을 여러 개의 프로세스로 구성하여 각 프로세스가 하나의 작업을 처리
- 하나의 프로세스가 잘못되어도 동작 가능
- 프로세스 간 공유하는 메모리가 없어서 Context Switching이 발생하면 데이터를 처음부터 불러와야 함
<br/>

#### 멀티 스레드

- 프로그램을 여러 개의 스레드로 구성하여 각 스레드가 작업을 처리하는 것
- 시스템 자원 소모 감소, 처리 비용 감소, 실행 속도 향상, 스레드 간 자원 공유
- 디버깅 어려움, 동기화나 교착 상태 이슈 발생, 하나의 스레드 오류로 전체 프로세스에 문제 발생
- 프로세스 밖에서 스레드 제어 불가
<br/>
  
## 참고자료

https://inpa.tistory.com/entry/%F0%9F%91%A9%E2%80%8D%F0%9F%92%BB-%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4-%E2%9A%94%EF%B8%8F-%EC%93%B0%EB%A0%88%EB%93%9C-%EC%B0%A8%EC%9D%B4#thankYou  
https://jaehoney.tistory.com/241
