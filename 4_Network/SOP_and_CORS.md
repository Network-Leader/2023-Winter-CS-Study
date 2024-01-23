# SOP & CORS

## 0. Origin

### 개념

![network_url](https://github.com/Network-Leader/2023-Winter-CS-Study/assets/49124725/26d6d346-5cb6-4f2a-8f00-16619f39e098)

- scheme, domain name, port 세 가지가 합쳐진 것
- 포트 번호의 경우, http://domain.com과 같이 생략되어 있다면 기본 포트를 기준으로 하고(HTTP의 경우 80, HTTPS의 경우 443), 포트가 명시되었다면 명시된 포트 번호가 기준  
   <br/>  

## 1. SOP

### 개념

- Same-Origin Policy (동일 출처 정책)
- 동일한 출처(origin)에서만 리소스를 공유할 수 있게끔 제한하는 **브라우저의 보안 정책**
- 출처가 서로 다른 애플리케이션끼리 통신하는 데에 아무런 제약이 없다면 악의적인 사용자가 CSRF 혹은 XSS 등의 공격을 통해 다른 사용자의 민감한 정보를 손쉽게 탈취 가능  
  <br/>  

### 제한

- fetch API 등을 이용하여 다른 출처로 요청을 날리는 것
- 자바스크립트 등을 이용하여 다른 출처의 iframe에 접근하는 것
- 자바스크립트 등을 이용하여 다른 출처의 이미지를 읽는 것  
  <br/>  

### 허용

- 다른 출처(cross-origin)의 스크립트를 문서에 삽입(embed)하는 것
- &lt;link&gt; 혹은 @import로 다른 출처의 css를 삽입하는 것
- X-Frame-Options 응답 헤더가 DENY 혹은 SAMEORIGIN이 아닌 이상, 일반적으로 다른 출처의 iframe을 삽입하는 것
- &lt;form&gt; 태그의 action 속성값으로 출처가 다른 URL을 사용하는 것(=다른 출처로 폼 데이터를 전송하는 것)
- 다른 출처의 이미지를 삽입하는 것
- 다른 출처의 오디오·비디오를 삽입하는 것  
  <br/>  

## 2. CORS

### 개념

- SOP 정책으로 인해 다른 출처의 자원을 사용할 수 없는 것을 개선하여 출처가 다른 리소스를 사용할 수 있도록 예외를 허용해주는 **브라우저 정책**
- CORS 정책을 지킨다면 SOP에서 기본적으로 제한하고 있는 행위들의 적용을 받지 않게 됨  
  <br/>  

### 동작

1. 웹 애플리케이션이 출처가 다른 곳에 요청할 때 요청 헤더에 Origin 이라는 필드를 함께 전송
   - Origin: https://www.google.com
2. 서버가 응답할 때 Access-Control-Allow-Origin 이라는 응답 헤더 필드에 허용하고자 하는 출처를 명시
   - 출처가 https://my-server.com인 서버에서 https://www.google.com로 부터 오는 리소스 요청을 허용하고자 한다면, 응답 헤더에 Access-Control-Allow-Origin: https://www.google.com 을 설정하여 응답
3. 응답을 받은 브라우저는 자신이 보냈던 요청의 Origin과 서버 응답의 Access-Control-Allow-Origin 값이 일치하는지를 살펴보고, 일치하면 출처가 다른 요청일지라도 유효한 요청으로 보고 받아온 리소스를 사용할 수 있게 허용  
   <br/>  

### 헤더

CORS 정책은 Origin 및 Access-Control- 헤더들을 통해 제어 가능

#### 요청 헤더

- Origin: 출처가 다른 요청 혹은 preflight 요청의 출처, 값이 null 일 수도 있으며, 출처가 다른 요청의 경우 항상 Origin 헤더가 전송
- Access-Control-Request-Method: preflight 요청을 보낼 때, 서버에게 실제 요청의 HTTP 메서드 정보 제공
- Access-Control-Request-Headers: preflight 요청을 보낼 때, 서버에게 실제 요청의 HTTP 헤더 정보 제공
  > preflight request: 실제 요청 전에 브라우저에서 보내는 작은 요청, 지금 요청을 보내는 프론트엔드가 백엔드 서버에서 허용한 Origin이 맞는지, 해당 엔드포인트에서 어떤 HTTP 메소드들을 허용하는지 등을 확인  
<br/>  

#### 응답 헤더

- Access-Control-Allow-Origin: 리소스에 접근할 수 있는 출처를 명시, 오직 하나의 출처를 명시하거나, 와일드카드(\*) 사용 가능
  - 인증 정보(credential)를 사용하는 경우 와일드카드를 사용할 수 없고, 반드시 하나의 출처를 명시
  - 헤더 값으로 와일드카드가 아니라 하나의 출처를 명시하는 경우, 출처를 Vary 헤더에도 명시하여 클라이언트에게 출처에 따라 응답이 달라질 수 있음을 명시
- Access-Control-Expose-Headers: 기본적으론 브라우저의 스크립트에 노출되지는 않지만, 브라우저 스크립트에서 접근할 수 있도록 허용하는 헤더
  - 커스텀 헤더를 포함하여 추가로 헤더를 스크립트에서 접근할 수 있도록 하고자 할 땐 Access-Control-Expose-Headers 응답 헤더를 사용
- Access-Control-Max-Age: preflight 요청이 얼마 동안 캐시 될지를 나타낼 때 사용, 헤더 값의 단위는 초
  - 파이어폭스의 경우 최대값은 86,400초(24시간), 크롬의 경우 버전 76 이전에는 최대 600초(10분), 버전 76 부터는 최대 7,200초(2시간)
- Access-Control-Allow-Credentials: 요청의 인증 모드(e.g. fetch API의 credentials)가 include인 경우, 응답을 브라우저의 스크립트에서 접근할 수 있도록 허용할지를 나타낼 때 사용, credentials가 include인 요청의 경우 Access-Control-Allow-Credentials 헤더 값이 true 이어야만 스크립트에서 응답에 접근 가능, 인증 정보(credential)에는 HTTP 쿠키, 인증 헤더, TLS 클라이언트 인증서 등이 포함
- Access-Control-Allow-Methods: preflight 요청에 대한 응답에 사용되는 헤더, 이후 본 요청에서 어떤 HTTP 메서드를 사용할 수 있는지를 나타낼 때 사용, 하나 이상의 HTTP 메서드를 **,** 로 구분하여 명시
- Access-Control-Allow-Headers: Access-Control-Request-Headers 헤더를 포함하는 preflight 요청에 대한 응답에 사용되는 헤더, 이후 본 요청에서 어떤 HTTP 헤더를 사용할 수 있는지를 나타낼 때 사용, Access-Control-Request-Headers 요청 헤더가 존재하는 경우 반드시 응답 헤더에 Access-Control-Allow-Headers를 포함  
  <br/>

### 동작 흐름

#### 간단한 요청(Simple Request)

아래 조건을 모두 만족해야 함

- HTTP 메서드가 GET, HEAD POST 중 하나인 경우
- 브라우저에 의해 자동으로 설정되는 헤더(e.g. Connection, User-Agent)등을 제외하고, 요청 헤더가 아래 목록에 나와있는 것만 설정된 경우
  - Accept, Accept-Language, Content-Language, Content-Type
    - Content-Type의 경우, 헤더값이 application/x-www-form-urlencoded, multipart/form-data, text/plain 중 하나

위 조건을 만족하는 요청은 별다른 절차 없이 다른 출처에 HTTP 요청을 보낼 수 있음, 일단 요청을 보내고 응답을 받은 뒤 해당 요청이 CORS를 만족하는지를 체크  
<br/>  

#### 복잡한 요청(Complex Request)

간단한 요청 이외의 요청

- 본 요청을 보내기 전에 preflight 요청을 보내서 다른 출처에 해당 요청을 보낼 수 있는지 점검한 뒤, 보낼 수 있다고 확인을 받으면 본 요청을 서버에 보냄
- preflight 요청은 OPTION HTTP 메서드를 사용
  - OPTIONS /data HTTP/1.1
- 이를 받은 서버에선 아래와 같이 허용하는 출처와 허용하는 메서드, preflight 요청을 얼마 동안 캐시 할 것인지 등에 관한 정보를 응답
- preflight 요청의 성공/실패 여부, 즉 preflight 요청에 대한 응답이 성공(200 OK)인지, 혹은 실패(400번대 코드)인지의 여부와 CORS 위반 에러는 상관 없음  
  <br/>  

#### Credential을 포함한 요청

HTTP 쿠키와 같이 인증 정보를 포함하는 요청, 기본적으로 fetch 등의 요청 API는 다른 출처에 요청하는 경우엔 쿠키 정보나 인증과 관련된 헤더를 요청에 포함하지 않음

- same-origin: 기본값으로, 같은 출처 간 요청에만 인증 정보를 포함
- include: 다른 출처에 요청하는 경우에도 항상 인증 정보를 포함
- omit: 인증 정보를 절대 포함하지 않음
- 다른 출처에 인증 정보를 포함하여 요청을 보내는 경우, 서버 측에선 반드시 Access-Control-Allow-Credentials 응답 헤더 값을 true로 설정, Access-Control-Allow-Origin 헤더 값에 반드시 하나의 출처를 명시  
  <br/>  
  
## 참고자료

https://velog.io/@jesop/SOP%EC%99%80-CORS  
https://jaehyeon48.github.io/web/sop-and-cors/
