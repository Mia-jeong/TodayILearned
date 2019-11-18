# Idempotence (멱등 법칙)

### 1. Idempotence란?

RESTFul Service 관점에서 Idempotence란 클라이언트에서 반복적으로 똑같은 내용을 서버에 요청해도 같은 결과를 생성한다는 것이다. 즉, 여러번의 동일한 요청을 보내도 하나의 요청을 보낸 것처럼 똑같은 영항을 가진다는 것이다. 

### 2. Idempotence in REST APIs

- `GET` : 
  - GET은 멱등 법칙에 속한다.
  - 여러번 요청해도 같은 결과를 가진다.
  - HTTP GET은 서버의 데이터를 변경하는데에 절대 사용되서는 안 된다.
- `PUT`:
  - PUT은 멱등 법칙에 속한다.
  - `같은 데이터` 로 여러번 업데이트를 해도 결과 값은 똑같다.
- `DELETE`:
  - HTTP spec에 따르면 DELETE역시 멱등 법칙에 속한다.
  - 만약 데이터를 실제로 지우는것이 아니라 데이터를 지웠다고 마킹할 경우 (ex: deleted: true/false) DELETE는 멱등 법칙에 속한다.
  - 실제로 데이터를 지운다면 이러한 요청은 멱등 법칙에 속하지 않는다.

### 3. NOT Idempotence in REST APIs

- `POST`:
  - POST는 멱등법칙에 속하지 않느다.
  - 여러번의 POST요청은 각각 다른 결과를 가져 올 것이다.
  - POST 는 `None-Idempotence` 로 사용 되길 권장 한다.

