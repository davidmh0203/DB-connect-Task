# 사용자 정보 저장을 위한 DB 연동 실습

---

## 목적

클라이언트-서버 웹 아키텍처 기반의 서비스에서 발생하는 데이터를 **안정적이고 효율적으로 저장하고 관리**하기 위해  
`DATABASE`를 생성하고, 이를 **서버와 연결하는 방법을 확인**하기 위한 실습입니다.

---

## 과정

### 1. 서버 만들기

- Node.js 기반의 `Express` 프레임워크를 활용해 기본 서버를 구성합니다.
- `/user`에 `POST` 요청 시 `id`, `pw`를 저장하고,  
  `/db`에 `GET` 요청 시 전체 유저 정보를 조회합니다.

---

### 2. DB 만들기

```sql
CREATE DATABASE minhyeong;

CREATE TABLE users (
  id VARCHAR(30) PRIMARY KEY, 
  pw VARCHAR(100)
);
```
<img width="680" alt="DB, Table 생성" src="https://github.com/user-attachments/assets/efdf4919-9810-4cc2-b267-3b1809ff3962" />

- 위 SQL문을 **MySQL Workbench**에서 실행하면 왼쪽 `Schemas` 탭에 `minhyeong` 데이터베이스와 `users` 테이블이 생성됩니다.
- SQL문 실행 후 새로 생성된 모습이 보이지 않는다면 **스키마 상단의 새로고침 버튼(🔄)** 을 눌러 확인할 수 있습니다.
<img width="213" alt="생성된 스키마" src="https://github.com/user-attachments/assets/4d7d9c1e-b29d-42c3-ad22-6f2783670de2" />

---

### 3. 서버와 DB 연결하기

- `mysql2` 모듈을 활용해 JavaScript 파일에서 DB에 접근합니다.
- DB 연결 설정 객체(`conn`)를 만들어 `host`, `user`, `password`, `database`를 입력한 후, `module.exports`로 내보냅니다.
- `app.js`에서는 `require('./mysql')`을 통해 연결하고,  
  `db.query()`를 사용해 SQL문을 실행합니다.

---

### 4. 연결한 DB 확인하기 (Postman 활용)

#### Postman 사용 이유

- REST API를 쉽게 테스트할 수 있는 **무료 도구**입니다.
- `GET`, `POST` 요청을 보내고, **응답 결과를 JSON 형식**으로 확인할 수 있습니다.

#### 사용 방법

1. Postman 접속 → `New → HTTP request` 버튼 클릭  
<img width="1278" alt="postman 첫 화면" src="https://github.com/user-attachments/assets/b0ae9a5e-f7a2-459a-ba3b-d8ed3d295ddf" />
<img width="1278" alt="postman http UI" src="https://github.com/user-attachments/assets/7dca1c3d-5ff3-485d-bc76-938995426f51" />

2. 요청 타입을 `POST`로 설정  <img width="1278" alt="postman get-  변경" src="https://github.com/user-attachments/assets/66a7fa66-5839-4f73-a7ed-fbb181688257" />

3. URL 입력: `http://localhost:3000/user`  <img width="1278" alt="postman get-  변경" src="https://github.com/user-attachments/assets/c60d1c7c-1f3f-4bef-a7d1-230ed788a22a" />

4. 상단 탭 중 `Body → raw → JSON` 선택  <img width="1278" alt="postman post-  body, raw" src="https://github.com/user-attachments/assets/d5d588b9-f596-464f-91ef-d2baaba3016a" />

5. 아래와 같은 JSON 데이터를 입력:

```json
{
  "id": "tester",
  "pw": "1234"
}
```

6. **[Send]** 버튼을 누르면 `200 OK`와 함께 저장이 성공한 응답을 확인할 수 있습니다.
<img width="1278" alt="postman post 성공 화면" src="https://github.com/user-attachments/assets/659ed3fa-6b8b-4a2d-ab4c-8ac3a5fa62e2" />

---

## 요약

- `id`, `pw` 등 로그인 정보를 저장하기 위해 MySQL을 활용한 DB와 서버를 연결했습니다.
- 연결이 잘 되었는지 확인하기 위해 **Postman**이라는 프로그램을 사용하여 `POST` 요청을 전송했습니다.
- `users` 테이블을 조회해 본 결과, **입력한 데이터가 정상적으로 저장된 것**을 확인할 수 있었습니다.

---

## 결과

> 결과 화면 캡처 이미지 (예시)

- POST 요청 성공  
  ![postman_post](./images/postman_post.png)

- GET 요청 결과  
  ![postman_get](./images/postman_get.png)

- 브라우저 확인  
  ![browser](./images/browser.png)

## 결과

- 사용자 저장 성공
- 사용자 목록 조회 성공
- 과제 요구사항 충족 + 캡처 완료
