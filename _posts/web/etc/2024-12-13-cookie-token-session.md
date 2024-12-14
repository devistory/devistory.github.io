---
title: 인증(Authentication)과 Cookie, Token, Session 
date: 2024-12-13 00:00:00 +09:00
description: 인증(Authentication)에 필요한 Cookie, Token, Session에 대해서 정리
categories: [WEB, Etc]
tags: [Secrurity, Cookie, Session, Token,]
hidden: false
image:
  path: /assets/img/logo/auth_logo.png
  alt: Authentication & Authorization
---

이 글은 로그인과 같은 사용자 `인증(authentication)`에 대한 내용과 해당 기능을 구현하면서 접하게 될 `Cookie`, `Token`, `Session`에 대하여 정리하고자 합니다.



## 쿠키(Cookie)란?
### 개념
- `Client(Browser)`에 저장되는 작은 데이터 파일
- HTTP 요청과 함께 자동으로 서버에 전송되어 사용자의 상태를 유지하거나 사용자 정보를 저장하는데 사용

### 특징
- `Server`가 `Client(Browser)`에 데이터를 저장하도록 요청
- `브라우저(Browser)`마다 저장되고, 사용자가 삭제하거나 만료될 때까지 유지됨
- 용량이 제한적, 일반적으로 도메인당 4KB

#### 장점
- `Client` 상태를 유지하는 간단한 방법
- `Client`에 저장되기 때문에 `Server`에 부담이 적음

#### 단점
- 보안 취약점: `Cookie`가 탈취되면 `Session hijacking` 공격 발생 가능
- 전송 데이터가 많아지면 요청 크기가 커질 수 있음

<br/>

---
## 세션(Session)이란?
### 개념
- `Client`와 `Server` 간 연결 상태를 유지하기 위한 `Server` 측 저장 방식
- `Server`에 `Client`별로 데이터를 저장하고 고유한 `Seesion ID`를 `Client`에 제공

### 특징
- `Server` Memory 또는 Database에 저장
- 일반적으로 `Cookie`에 `Session ID`를 저장하거나 URL에 포함하여 `Client`를 식별
- `Client(Browser)`를 닫거나 지정된 시간이 지나면 `Session`이 만료됨

#### 장점
- `Client`에 민감한 데이터를 저장하지 않아 비교적 안전함
- `Server`에서 데이터 제어 가능

#### 단점
- `Session`이 많아지면 저장 공간 부담 및 서버 부하
- `Scaling(load balancers)` 시 추가 작업 필요

<br/>

---
## 토큰(Token)이란?
### 개념
- 사용자를 인증하기 위한 문자열
- 일반적으로 JSON Web Token(JWT) 형식이 많이 사용됨
- `Client`가 `Server`로부터 인증 받은 후 발급 받아 요청마다 인증 정보를 포함

### 특징
- `Client`에 저장되고, 이후 요청 시 `Header`에 포함
    ``` html
    Authorization: Bearer <token>
    ```
- `토큰(Token)`에는 `서명(Signature)`이 있어서 변조를 방지할 수 있음
  
#### 장점
- `Server`는 상태 유지하지 않아 확장성이 좋음(`Stateless`)
- 다양한 클라이언트(웹, 모바일 앱 등)에서 사용 가능
- JWT는 자체적으로 인증 정보 및 권한을 포함

#### 단점
- `토큰(Token)`이 만료되기 전에는 강제로 무효화하기 어려움
- `토큰(Token)`이 탈취되면 제3자가 인증을 가장할 수 있음
- `토큰(Token)` 길이가 늘어날수록 네트워크 부하


## 쿠키, 세션, 토큰 비교

| 특징      | 쿠키                   | 세션                          | 토큰                           |
| --------- | ---------------------- | ----------------------------- | ------------------------------ |
| 저장 위치 | Client                 | Server                        | Client                         |
| 보안      | 취약(HTTPS로 보완)     | 비교적 안전                   | 보안 문제는 Client 관리가 중요 |
| 유지 방식 | 자동 전송              | Server에서 상태 유지          | Client가 직접 관리             |
| 확장성    | 제한적                 | Server에 부담                 | 매우 좋음                      |
| 사용 예시 | 상태 저장, 자동 로그인 | 로그인 세션, 사용자 상태 유지 | API 인증, 모바일 앱 인증       |

<br/>

---
## 어떻게 사용해야 할까?
- `쿠키(Cookie)`는 간단한 데이터 저장
  - 로그인 정보 저장
  - 쇼핑몰의 장바구니 데이터
- `세션(Session)`은 보안이 중요한 로그인 상태 관리에 유용
  - `Server`에서 `Session ID`로  `Client`를 식별하고 상태 유지
  - `Server`에서 관리되기 떄문에 비교적 안전
- `토큰(Token)`은 API 기반 시스템에서 `인증` 및 권한 관리에 적합
  - `Stateless`하기 때문에 서버의 확장 및 분산된 환경에 유용

<br/>

---
## 인증(Authentication), 인가(Authorization)
### 인증(Authentication)과 인가(Authorization)란?
- `인증(Authentication)` : 사용자가 누구인지 식별하는 과정
- `인가(Authorization)` : 인증된 사용자가 특정 리소스나 기능에 접근할 수 있는 권한이 있는지 확인하는 과정

#### 인증, 인가 비교

| 특징      | 인증(Authentication)                | 인가(Authorization)                       |
| --------- | ----------------------------------- | ----------------------------------------- |
| 질문      | 누구인가?                           | 무엇을 할 수 있는가?                      |
| 목적      | 사용자 신원 확인                    | 권한 확인 및 자원 접근 통제               |
| 순서      | 인증이 먼저 수행                    | 인증 후에 수행                            |
| 결과      | 사용자가 신뢰할 수 있는지 여부 결정 | 사용자가 리소스에 접근 가능한지 여부 결정 |
| 기술      | 비밀번호, 생체인식, 인증 토큰 등    | 역할 기반 제어(RBAC), 권한 정책 등        |
| 적용 대상 | 모든 사용자                         | 인증된 사용자만                           |
| 예시      | 로그인 성공                         | 관리자만 이 페이지에 접근할 수 있습니다.  |

<br/>

### 세션(Session) 인증, 토큰(Token) 인증
#### 세션(Session) 인증
- `세션(Session) 인증`은 사용자가 로그인하면 `Server`가 `Session`을 생성하여 사용자 정보를 저장하고, `Client`는 `Seesion ID`를 통해 `Server`와 상호작용하는 방식입니다.

<br/>

##### 작동 방식

![Session authentication](/assets/img/posts/web/etc/auth/auth_01.png)
_Session authentication_

1. 사용자(`Client`)가 인증 정보(ID/PW, 지문 등)와 함께 인증 요청
2. `Server`는 인증 정보와 일치하는 정보 확인
3. 인증 결과에 따른 처리
   - 인증 정보 불일치 : 인증 실패 메세지 전달
   - 인증 정보 일치 : `세션 ID(Session ID)` 생성, 서버 메모리 또는 Database에 저장
4. `Client`로 `세션 ID`를 전달(일반적으로 Cookie에 담아 전달)
5. `Client`는 `세션 ID` 저장
6. `Server`로 요청할 때 `세션 ID`를 함께 담아서 요청
7. `Server`는 `세션 ID`로 사용자 정보 확인
8. 일치하는 정보가 있으면 `Client`로 정보 전달

<br/>

#### 세션(Session) 인증 단점
- `세션 ID` 자체는 유의미한 정보가 없지만 `Session Hijacking`에 의해서 `세션 ID`를 탈취한다면 서버에 접근이 가능합니다.
  - 대응 방법 : `세션`을 `Server`에서 관리하기 때문에 탈취된 `세션`정보를 지우면 접근을 막을 수 있습니다.

![Session drawbacks](/assets/img/posts/web/etc/auth/auth_02.png)
_Session drawbacks_

> **참고 사항**<br/>
> **Session Hijacking이란?**<br/>
> 공격자가 두 시스템 중간에서 세션을 <u>훔치거나 유추</u>하여, 시스템에 접근하는 공격<br/>
> 발생 원인은 다음과 같습니다.<br/>
> \- 취약한 세션ID 생성 알고리즘 사용<br/>
> \- 암호화되지 않은 일반 텍스트로 전송<br/>
> \- 짧은 세션ID
{: .prompt-info }


<br/>

- `세션`을 저장하여 관리하기 때문에 요청이 많아지면 `Server`에 부하가 심해진다.
  - 대응 방법 : `Server`를 늘려서 요청을 분산 시킬 수 있겠지만 `세션` 관리가 복잡해집니다. `세션` 정보를 공유하기 위해서 **공용 저장소**를 만들 수 있겠지만 이 또한 부하의 point만 다른 것이지 해결 책은 아닙니다. 이런 경우에는 `토큰(token) 인증` 방식이 적합합니다.

![Session drawbacks](/assets/img/posts/web/etc/auth/auth_03.png)
_Session drawbacks_

<br/>

#### 토큰(token) 인증
- `토큰(token) 인증`은 사용자가 로그인하면 `Server`가 인증 토큰(일반적으로 JWT)을 발급하고, `Client`가 이후 요청에서 `토큰(token)`을 전송하여 인증받는 방식입니다.
- `토큰(token)` 자체에 사용자 정보를 포함하거나 인증 상태를 나타냅니다.

<br/>

##### 작동 방식

![Token authentication](/assets/img/posts/web/etc/auth/auth_04.png)
_Token authentication_

1. 사용자(`Client`)가 인증 정보(ID/PW, 지문 등)와 함께 인증 요청
2. `Server`는 인증 정보와 일치하는 정보 확인
3. 인증 결과에 따른 처리
   - 인증 정보 불일치 : 인증 실패 메세지 전달
   - 인증 정보 일치 : `토큰(token)` 생성
4. `Client`로 `토큰(token)`를 전달(일반적으로 Cookie에 담아 전달)
5. `Client`는 `토큰(token)` 저장(LocalStorage, SessionStorage 또는 Http-only 쿠키에 저장)
6. `Server`로 요청할 때 `토큰(token)`를 함께 담아서 요청
7. `Server`는 `토큰(token)`의 `서명(signature)`으로 위변조를 검증하고 사용자 정보 확인
8. 일치하는 정보가 있으면 `Client`로 정보 전달

<br/>

##### 토큰(Token) 인증 단점
- `토큰(token)`의 정보는 암호화되지 않았기 때문에 쉽게 내용을 확인할 수 있습니다.
- `토큰(token)`이 탈취되면 만료되기 전까지는 재사용 가능합니다.
- 발급된 `토큰(token)`은 `Server`에서 상태를 저장하지 않기(Stateless) 때문에 만료 전까지는 `토큰(token)`을 무효화하기 어렵습니다.

  - 대응 방법 : 근본적으로 `토큰(token)`을 무효화할 수 있는 방법은 없지만 몇가지 대응 방법에 대해서 정리하였습니다.
    - 방법 1 : 민감한 정보 제외, 토큰 탈취를 막기위해 안전하게 관리<br/>(LocalStorage, SessionStorage 또는 Http-only 쿠키를 사용)
    - 방법 2 : `black list`를 사용하여 탈취된 `토큰`을 차단<br/>(server에서 관리하기 때문에 session 인증과 다를게 없기 때문에 token의 장점이 없음)
    - 방법 3 : `access token`의 만료기간을 짧게 만들어 재사용할 수 있는 시간을 짧게 합니다.<br/>(접근 시간이 짧은 것이지 근본적 해결 방법은 아님)
    - 방법 4 : `refresh token`이 탈취 당하면 `access token`을 재발급 받으면 되기 때문에 만료기간을 짧게해도 `방법3`은 무의미합니다. <br/>`access token`을 재발급할 때 마다 `refresh token`을 일회용으로 사용하면 `refresh token`이 탈취되더라도 방어할 수 있습니다. 이러한 방법을 `refresh token rotation`이라 합니다.

<br/>

---
## 마무리

`인증(Authentication)`과 `인가(Authorization)`, `Cookie`, `Session`, `Token` 대해서 정리하였습니다. 해당 내용 이외에 더 많은 내용이 필요하시면 `참고 자료`를 참조하시면 됩니다.

<br/>

📑 **참고 자료**
- [Inpa Dev 블로그](https://inpa.tistory.com/entry/WEB-📚-JWTjson-web-token-란-💯-정리#cookie_/_session_/_token_인증_방식_종류)
- [노마드 코더(세션 vs 토큰 vs 쿠키? 기초개념 잡아드림. 10분 순삭!)](https://youtu.be/tosLBcAX1vk?si=cCURG1sIsnLT4dy5)
- [얄팍한 코딩사전(쿠키, 세션, 캐시가 뭔가요?)](https://youtu.be/OpoVuwxGRDI?si=QQ5j9xNxpMy0SGaE)
- [코딩애플(JWT 대충 쓰면 님들 코딩인생 끝남)](https://youtu.be/XXseiON9CV0?si=M4wS4LtI2g4jBKiI)

<br/>


> 🔖 **이미지 출처**<br/>
> Icons made by various authors from [www.flaticon.com](https://www.flaticon.com)
> - Icon made by Freepik from www.flaticon.com
> - Icon made by Smashicons from www.flaticon.com
> - Icon made by Iconjam from www.flaticon.com
> - Icon made by yaicon from www.flaticon.com
> - Icon made by kliwir art from www.flaticon.com
> - Icon made by Alfredo Hernandez from www.flaticon.com
> - Icon made by Creative Squad from www.flaticon.com
> - Icon made by Mihimihi from www.flaticon.com
> - Icon made by Chanut-is-Industries from www.flaticon.com
> 
>*Thanks to the creators who created these great icons.*

<br/>
> 해당 글은 잘못되거나 새로운 내용이 확인되면 언제든 수정될 수 있습니다.
{: .prompt-info }
<br/>
