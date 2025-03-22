# 웹 기초

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
