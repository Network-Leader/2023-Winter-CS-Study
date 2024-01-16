### 논리적 주소와 물리적 주소의 차이점에 대해 설명해주세요

프로그램 관점에서 논리적 주소는 CPU가 생성하는 것이지만 물리적 주소는 실제 메모리 위치에 존재하는 것

# **Logical address 와 Physical Address**

### **Logical address**(논리적 주소)

프로세스마다 독립적으로 가지는 주소 공간

각 프로세스마다 0번지부터 시작

CPU가 보는 주소는 logical address이다

- 프로그램의 실행 과정
    1. 프로그램을 메모리 가져와서 프로세스 문맥에 배치하고,
    2. 해당 시점에 이용 가능한 CPU에서 실행한다.
    3. 그렇게 **프로세스가 실행되면 메모리에서 명령이나 데이터에 엑세스를 하는데,**
       이 실행 과정에서 프로그램만의 **독자적인 주소 공간**이 형성

### **Physical address**(물리 주소)

메모리에 실제 올라가는 위치

사용자는 실제 메모리에 접근 안함. OS가 관리

## **주소 바인딩**

주소 바인딩이란 주소를 결정하는 것을 의미. 논리적 주소가 물리적 주소로 올라가는 과정.

### **Compile time binding**

- 물리적 메모리 주소가 컴파일 시 주소변환
- 시작 위치 변경시 재컴파일
- 컴파일러는 절대 코드를 생성

### **Local time bining**

- 프로그램의 실행이 시작될 때 주소 변환이 이루어지는 방법
- Loader의 책임하의 물리적 메모리 주소를 부여
- 컴파일러가 이진 코드를 재배치 가능 코드(relocatable code)로 만든 경우 가능

### **Execution time bining(런타임 바인딩)**

- 프로그램이 시작된 이후, 즉 실행 중에 주소 변환이 이루어지는 방법
- 수행이 시작된 이후에도 프로세스의 메모리 상 위치를 옮길 수 있음
- CPU가 주소를 참조할 때마다 binding을 점검(address mapping table) → 하드웨어적인 지원이 필요(MMU)

## **Memory-Management Unit (MMU)**

![os_address_binding.png](img%2Fos_address_binding.png)

논리적인 주소를 물리적인 주소로 매핑해주는 하드웨어

주소변환을 지원해주는 하드웨어

런타임 바인딩은 프로그램 실행 중에도 계속 주소가 바뀔 수 있어야 하기 때문에, CPU가 메모리 주소를 요청할 때마다 그때마다 바인딩을 체크하고 주소 변환을 해줘야 한다.

- **MMU scheme**: 사용자 프로세스가 CPU에서 수행되며 생성해내는 모든 주소값에 대해 base register의 값을 더한다.
- **user program**: 논리적인 주소만을 다루며, 실제 physical address를 볼 수 없으며 알 필요도 없다.

### 참고자료

[https://systorage.tistory.com/entry/CS-운영체제-메모리-관리#주소 바인딩-1](https://systorage.tistory.com/entry/CS-%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EA%B4%80%EB%A6%AC#%EC%A3%BC%EC%86%8C%20%EB%B0%94%EC%9D%B8%EB%94%A9-1)

[https://velog.io/@effirin/CS-메인-메모리](https://velog.io/@effirin/CS-%EB%A9%94%EC%9D%B8-%EB%A9%94%EB%AA%A8%EB%A6%AC)