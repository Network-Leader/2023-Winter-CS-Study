# API, REST, REST API

## 1. API(Application Programming Interface)

* API는 다른 소프트웨어 시스템과 통신하기 위해 따라야 하는 규칙을 의미합니다.
* API 아키텍처는 일반적으로 클라이언트와 서버 측면에서 설명됩니다. 요청을 보내는 애플리케이션을 클라이언트라고 하고 응답을 보내는 애플리케이션을 서버라고 합니다. 
  * 날씨 예에서 기상청의 날씨 데이터베이스는 서버이고 모바일 앱은 클라이언트입니다. 

API가 생성된 시기와 이유에 따라 API는 네 가지 방식으로 작동할 수 있습니다.

### SOAP API 

이 API는 단순 객체 접근 프로토콜을 사용합니다. 클라이언트와 서버는 XML을 사용하여 메시지를 교환합니다. 과거에 더 많이 사용되었으며 유연성이 떨어지는 API입니다.

### RPC API

이 API를 원격 프로시저 호출이라고 합니다. 클라이언트가 서버에서 함수나 프로시저를 완료하면 서버가 출력을 클라이언트로 다시 전송합니다.

### Websocket API

[Websocket API](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-websocket-api-overview?pg=wianapi&cta=websocketapi)는 JSON 객체를 사용하여 데이터를 전달하는 또 다른 최신 웹 API 개발입니다. WebSocket API는 클라이언트 앱과 서버 간의 양방향 통신을 지원합니다. 서버가 연결된 클라이언트에 콜백 메시지를 전송할 수 있어 REST API보다 효율적입니다.

### REST API

오늘날 웹에서 볼 수 있는 가장 많이 사용되고 유연한 API입니다. 클라이언트가 서버에 요청을 데이터로 전송합니다. 서버가 이 클라이언트 입력을 사용하여 내부 함수를 시작하고 출력 데이터를 다시 클라이언트에 반환합니다. 아래에서  REST API에 대해 더 자세히 살펴보겠습니다.



## 2. REST(REpresentational State Transfer)

* REST란 자원을 이름으로 구분하여 해당 자원의 상태를 주고 받는 모든 것을 의미합니다.
* 즉, **HTTP URI(Uniform Resource Identifier)**를 통해 자원(Resource)를 명시하고, **HTTP Method**(POST, GET, PUT, DELETE, PATCH 등)를 통해 해당 자원 (URI)에 대한 CRUD Operation을 적용하는 것을 의미합니다.

> CRUD: 대부분의 컴퓨터 소프트웨어가 가지는 기본적인 데이터 처리 기능인 **Create(생성), Read(읽기), Update(갱신), Delete(삭제)**를 묶어서 일컫는 말이다.

### CRUD Operation이란
- Create, Read, Update, Delete를 묶어서 일컫는 말
- REST에서의 CRUD Operation 동작 예시는 다음과 같습니다.
  - Create: 데이터 생성(POST)
  - Read: 데이터 조회(GET)
  - Update: 데이터 수정(PUT, PATCH)
  - Delete: 데이터 삭제(DELETE)


### REST 구성 요소
- 자원(Resouce) : HTTP URI
- 자원에 대한 행위(Verb) : HTTP Method
- 자원에 대한 행위의 내용(Representations) : HTTP Message Pay Load

### REST의 장단점  

**장점**  

1. HTTP 프로토콜의 표준을 최대한 활용하여 여러 추가적인 장점을 함께 가져갈 수 있게 해 준다.
2. HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능하다.
3. REST API 메시지가 의도하는 바를 명확하게 나타내므로 의도하는 바를 쉽게 파악할 수 있다.
4. 여러 가지 서비스 디자인에서 생길 수 있는 문제를 최소화한다.
5. 서버와 클라이언트의 역할을 명확하게 분리한다.

**단점**  

1. HTTP Method 형태가 제한적이다.
2. 브라우저를 통해 테스트할 일이 많은 서비스라면 쉽게 고칠 수 있는 URL보다 Header 정보의 값을 처리해야 하므로 전문성이 요구된다.
3. 구형 브라우저에서 호환이 되지 않아 지원해주지 못하는 동작이 많다.(인터넷 익스플로러 등)

### REST 아키텍처 스타일의 몇 가지 원칙

1. Uniform Interface(균일한 인터페이스)
2. Stateless(무상태)
3. Layered System(계층화 시스템)
4. Cacheable(캐시 가능성)
5. Code-On-Demand(온디맨드 코드)





## 3. REST API  

 REST API는 *REST(REpresentational State Transfer)* 아키텍처 스타일의 디자인 원칙을 준수하는 API입니다.

### REST API 설계 예시  

1. URI는 명사, 소문자를 사용해야한다.
```
Bad Example http://lsh98.com/Studying/
Good Example http://lsh98.com/study/
```
2. 마지막에 슬래시(/) 포함하지 않는다.
```
Bad Example http://lsh98.com/study/
Good Example http://lsh98.com/study
```
3. 언더바 대신 하이폰을 사용한다.
```
Bad Example http://lsh98.com/study_blog
Good Example http://lsh98.com/study-blog
```
4. 파일 확장자는 URI에 포함하지 않는다.
```
Bad Example http://lsh98.com/photo.png
Good Example http://lsh98.com/photo
```
5. 행위를 포함하지 않는다.
```
Bad Example http://lsh98.com/delete-post/1
Good Example http://lsh98.com/post/1
```





## 4. RESTful

* RESTful은 REST 원칙을 준수하는 시스템을 의미합니다.

* RESTful 웹 서비스는 REST 아키텍처 스타일을 따르는 웹 서비스로, 쉽고 일관된 방식으로 리소스에 접근할 수 있게 합니다. 

* 하지만 REST를 사용했다 하여 모두가 RESTful한 것은 아닙니다. 
* REST API의 설계 규칙을 올바르게 지킨 시스템을 RESTful 하다 말할 수 있으며, 모든 CRUD 기능을 POST로 처리하는 API혹은 URI 규칙을 올바르게 지키지 않은 API는 REST API를 사용하였지만 RESTful 하지 못한 시스템이라 말할 수 있습니다.

### RESTful API 작동원리
* RESTful API의 기본 기능은 인터넷 브라우징과 동일합니다. 
* 클라이언트는 리소스가 필요할 때  API를 사용하여 서버에 접속합니다. API 개발자는 서버 애플리케이션 API 문서에서 클라이언트가 REST API를 어떻게 사용해야 하는지 설명합니다. 

다음은 모든 REST API 호출에 대한 일반 단계입니다.

1. 클라이언트가 서버에 요청을 전송합니다. 클라이언트가 API 문서에 따라 서버가 이해하는 방식으로 요청 형식을 지정합니다.
2. 서버가 클라이언트를 인증하고 해당 요청을 수행할 수 있는 권한이 클라이언트에 있는지 확인합니다.
3. 서버가 요청을 수신하고 내부적으로 처리합니다.
4. 서버가 클라이언트에 응답을 반환합니다. 응답에는 요청이 성공했는지 여부를 클라이언트에 알려주는 정보가 포함됩니다. 응답에는 클라이언트가 요청한 모든 정보도 포함됩니다.

REST API 요청 및 응답 세부 정보는 API 개발자가 API를 설계하는 방식에 따라 약간씩 다릅니다.

### RESTful API 클라이언트 요청 구성 요소

#### 고유 리소스 식별자

* 서버는 고유한 리소스 식별자로 각 리소스를 식별합니다. REST 서비스의 경우 서버는 일반적으로 URL(Uniform  Resource Locator)을 사용하여 리소스 식별을 수행합니다. URL은 리소스에 대한 경로를 지정합니다. URL은  웹페이지를 방문하기 위해 브라우저에 입력하는 웹 사이트 주소와 유사합니다. URL은 요청 엔드포인트라고도 하며 클라이언트가  요구하는 사항을 서버에 명확하게 지정합니다.

#### 메서드

* 개발자는 종종 HTTP(Hypertest Transfer Protocol)을 사용하여 RESTful API를 구현합니다. HTTP Method는 리소스에 수행해야 하는 작업을 서버에 알려줍니다. 

#### GET

* 클라이언트는 GET을 사용하여 서버의 지정된 URL에 있는 리소스에 액세스합니다. GET 요청을 캐싱하고 RESTful API 요청에 파라미터를 넣어 전송하여 전송 전에 데이터를 필터링하도록 서버에 지시할 수 있습니다.

#### POST

* 클라이언트는 POST를 사용하여 서버에 데이터를 전송합니다. 여기에는 요청과 함께 데이터 표현이 포함됩니다. 동일한 POST 요청을 여러 번 전송하면 동일한 리소스를 여러 번 생성하는 부작용이 있습니다.

#### PUT

* 클라이언트는 PUT을 사용하여 서버의 기존 리소스를 업데이트합니다. POST와 달리, RESTful 웹 서비스에서 동일한 PUT 요청을 여러 번 전송해도 결과는 동일합니다.

#### DELETE

* 클라이언트는 DELETE 요청을 사용하여 리소스를 제거합니다. DELETE 요청은 서버 상태를 변경할 수 있습니다. 하지만 사용자에게 적절한 인증이 없으면 요청은 실패합니다.

#### HTTP Header

* 요청 헤더는 클라이언트와 서버 간에 교환되는 메타데이터입니다. 예를 들어, 요청 헤더는 요청 및 응답의 형식을 나타내고 요청 상태 등에 대한 정보를 제공합니다.

#### 데이터

* REST API 요청에는 POST, PUT 및 기타 HTTP 메서드가 성공적으로 작동하기 위한 데이터가 포함될 수 있습니다.

#### 파라미터

* RESTful API 요청에는 수행해야 할 작업에 대한 자세한 정보를 서버에 제공하는 파라미터가 포함될 수 있습니다. 다음은 몇 가지 파라미터 유형입니다.
  - URL 세부정보를 지정하는 경로 파라미터.
  - 리소스에 대한 추가 정보를 요청하는 쿼리 파라미터.
  - 클라이언트를 빠르게 인증하는 쿠키 파라미터.



### RESTful API 인증 방법이란 무엇일까요?
RESTful 웹 서비스는 응답을 보내기 전에 먼저 요청을 인증해야 합니다. 인증은 신원을 확인하는 프로세스입니다. 예를  들어, 신분증이나 운전면허증을 제시하여 신원을 증명할 수 있습니다. 마찬가지로 RESTful 서비스 클라이언트는 신뢰를 구축하기  위해 서버에 자신의 신원를 증명해야 합니다.

RESTful API에는 4가지의 일반적인 인증 방법이 있습니다.

### HTTP 인증

HTTP는 REST API를 구현할 때 직접 사용할 수 있는 일부 인증 체계를 정의합니다. 다음은 이러한 체계 중 두 가지입니다.

1. 기본 인증

* 기본 인증에서 클라이언트는 요청 헤더에 사용자 이름과 암호를 넣어 전송합니다. 안전한 전송을 위해 이 페어를 64자의 세트로 변환하는 인코딩 기술인 base64로 인코딩합니다.

2. 전달자 인증

* 전달자(bearer) 인증이라는 용어는 토큰 전달자에 대한 액세스 제어를 제공하는 프로세스를  나타냅니다. 일반적으로 전달자 토큰은 서버가 로그인 요청에 대한 응답으로 생성하는 암호화된 문자열입니다. 클라이언트는 리소스에  액세스하기 위해 요청 헤더에 토큰을 넣어 전송합니다.

### API 키

API 키는 REST API 인증을 위한 또 다른 옵션입니다. 이 접근 방식에서 서버는 고유하게 생성된 값을 최초 클라이언트에 할당합니다. 클라이언트는 리소스에 액세스하려고 할 때마다 고유한 API 키를 사용하여 본인을 검증합니다. API 키의 경우 클라이언트가 이 키를 전송해야 해서 네트워크 도난에 취약하기 때문에 덜 안전합니다.

### OAuth

OAuth는 모든 시스템에 대해 매우 안전한 로그인 액세스를 보장하기 위해 암호와 토큰을 결합합니다.  서버는 먼저 암호를 요청한 다음 권한 부여 프로세스를 완료하기 위해 추가 토큰을 요청합니다. 특정 범위와 수명으로 언제든지 토큰을 확인할 수 있습니다.





### RESTful API 서버 응답에는 무엇이 포함되어 있나요?

REST 원칙에 따라 서버 응답에 다음과 같은 주요 구성 요소를 포함해야 합니다.

### 상태 표시줄

상태 표시줄에는 요청 성공 또는 실패를 알리는 3자리 상태 코드가 있습니다. 예를 들어, 2XX 코드는 성공을 나타내고 4XX 및 5XX 코드는 오류를 나타냅니다. 3XX 코드는 URL 리디렉션을 나타냅니다.

다음은 몇 가지 일반적인 상태 코드입니다.

- 200: 일반 성공 응답
- 201: POST 메서드 성공 응답
- 400: 서버가 처리할 수 없는 잘못된 요청
- 404: 리소스를 찾을 수 없음

### 메시지 본문

응답 본문에는 리소스 표현이 포함됩니다. 서버는 요청 헤더에 포함된 내용을 기반으로 적절한 표현 형식을 선택합니다. 클라이언트는 데이터 작성 방식을 일반 텍스트로 정의하는 XML 또는 JSON 형식으로 정보를 요청할 수 있습니다.  예를 들어, 클라이언트가 John이라는 사람의 이름과 나이를 요청하면 서버는 다음과 같이 JSON 표현을 반환합니다.

'{"name":"John", "age":30}'

### 헤더

응답에는 응답에 대한 헤더 또는 메타데이터도 포함됩니다. 이는 응답에 대한 추가 컨텍스트를 제공하고 서버, 인코딩, 날짜 및 콘텐츠 유형과 같은 정보를 포함합니다.


## 예상 질문
#### Q1. REST API의 개념에 대해서 설명해주세요. 이 때, REST의 개념도 함께 말해주세요

#### Q2. API의 개념에 대해서 설명해주세요.

#### Q3. REST API 설계 예시를 아는 대로 말해주세요.




## 참고 자료
https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html

https://aws.amazon.com/ko/what-is/restful-api/

https://aws.amazon.com/ko/what-is/api/
