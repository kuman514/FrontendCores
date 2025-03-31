# 웹 기초

## HTTP 상태 코드 (HTTP Status Code)
- 응답 코드란?
  - 통신의 결과를 나타내는 코드.
- 응답 코드를 사용해야 하는 이유?
  - 올바른 응답 코드 작성은 개발자에게 어떤 결과가 나타났는지 간결하고 명확하게 알려주는 이정표가 된다.
- 응답 코드의 종류와 그 의미
  - 1xx: 진행 중 정보 제공
  - 2xx: 성공적인 결과
  - 3xx: 리다이렉션
  - 4xx: 사용자 측 오류
  - 5xx: 서버 측 오류
- 자세한 내용은
  - https://datatracker.ietf.org/doc/html/rfc2616#section-10
  - https://developer.mozilla.org/ko/docs/Web/HTTP/Reference/Status

## Same Origin Policy (동일 출처 정책)
- 통신으로 데이터를 주고받을 때 출처(Origin)이 동일해야 한다는 정책이다. 이를 어기면 CORS Error가 발생한다.
- 이 때, 출처(Origin)은 프로토콜+도메인명+포트번호를 말하는 것이다.
- 예시
  - `https://yasuomaverick.com:8080/koishi`인 출처는 `https://yasuomaverick.com:8080`과 데이터를 주고받을 수 있다.
  - `https://koishi.com/`인 출처는 `https://yasuomaverick.com/`과 도메인이 달라 데이터를 주고받을 수 없다.
  - `ftp://yasuomaverick.com/`인 출처는 `https://yasuomaverick.com/`과 프로토콜이 달라 데이터를 주고받을 수 없다.
  - `https://yasuomaverick.com:8000/`인 출처는 `https://yasuomaverick.com:8080/`과 포트번호가 달라 데이터를 주고받을 수 없다.

## CORS (Cross Origin Resource Sharing)
- 서로 다른 두 출처(Origin, 프로토콜+도메인명+포트번호)가 데이터를 주고받을 수 있도록 서버가 허락해주는 HTTP 헤더 기반 메커니즘이다.
- 다른 출처에게 요청하는 방법
  - 출처가 서버 측에서 반환한 Access-Control-Allow-Origin 헤더값에 해당
  - OPTIONS 메소드를 통해, 허용되는 출처나 메소드나 헤더 등등을 사전 조사

## Base64
- Base64란?
  - 바이너리 데이터를 어떤 문자 코드에도 영향을 받지 않는 공통된 ASCII 문자로 표현한 인코딩.
  - 64진법을 사용한다.
- 작동 원리
  - 바이너리 데이터를 3바이트(즉 8 * 3 = 24비트)씩 붙이고, 그 묶음을 4마디로 쪼개어, 각 마디(6비트)의 값에 대응하는 ASCII 문자로 변환한다.
  - `ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789`와 `+ 또는 -` 그리고 `/ 또는 _` 등의 64문자로 표현된다.
  - 3바이트 미만의 패딩은 `=`로 표현된다.
- 왜 Base64를 사용하는가?
  - 바이너리 데이터를 텍스트로 다룰 수 있기 때문이다.
  - 기존 ASCII 문자 체계는 바이너리 데이터를 전송하기에 안전하지 않다. 제어문자나 특수문자를 해석하는 방식이 OS마다 다를 수 있기 때문이다.
  - 그러나, ASCII 문자 중 대소문자 / 숫자 / 텍스트 특수문자 등등을 활용하면 어떤 OS, 어떤 charset을 사용해도 안전한 인코딩이 가능하다. 
- 사용되는 예시
  - HTML에 포함된 작은 이미지나 아이콘
  - API 응답에서 이진 데이터 전송
  - 이메일 첨부 파일 인코딩 등등
