---
title: 간단한 REST API 서버(with:JSON Server)
date: 2024-12-25 00:00:00 +09:00
description: json-server로 간단한 REST API server 구축
categories: [Web, Etc]
tags: [Front-End, json-server]
hidden: false
image:
  path: /assets/img/logo/json_server_logo.png
  alt: json-server
---


이 글은 `json 파일`을 사용하여 RESTful API Server를 구축하는 내용입니다.<br/>
`Back-End`를 직접 구현하지 않고 `json-server`를 사용하여 간단한 테스트 서버를 구축하는 내용에  대하여 정리하고자 합니다.

## json-server란?
`json-server`는 JSON파일을 이용하여 간단한 RESTful API Server를 구축할 수 있는 도구입니다.<br/>
직접 `Back-End`를 구축할 필요가 없어서 `Front-End` 공부 혹은 프로토타입 개발에 활용할 수 있습니다.

<br/>

---

## 설치 방법

- json server 설치

```shell
npm install json-server
```
<br/>

- json 파일 준비
 
```json
{
    "animals": [
    { "id": 1, "name": "dog" },
    { "id": 2, "name": "cat" },
    { "id": 3, "name": "elephant" },
    { "id": 4, "name": "lion" },
    { "id": 5, "name": "tiger" }
    ],
    "fruits": [
    { "id": 1, "name": "apple" },
    { "id": 2, "name": "banana" },
    { "id": 3, "name": "cherry" },
    { "id": 4, "name": "grape" },
    { "id": 5, "name": "orange" }
    ],
    "jobs": [
    { "id": 1, "name": "teacher" },
    { "id": 2, "name": "engineer" },
    { "id": 3, "name": "doctor" },
    { "id": 4, "name": "artist" },
    { "id": 5, "name": "pilot" }
    ],
    "colors": [
    { "id": 1, "name": "red" },
    { "id": 2, "name": "blue" },
    { "id": 3, "name": "green" },
    { "id": 4, "name": "yellow" },
    { "id": 5, "name": "purple" }
    ]
}
```
{: file="data.json" }

<br/>

- json 실행
  - json-server --watch `[json파일 경로]` --port `[port번호]`

```shell
json-server --watch ./data.json --port 3000
```


![json-server start](/assets/img/posts/web/etc/json_server/json_server_02.png)
_json-server start_

<br/>

---

## 사용 방법
- 브라우저 접속하여 주소창에 localhost:3000/animals

![json-server test](/assets/img/posts/web/etc/json_server/json_server_03.png)
_json-server test_

> **참고 사항**<br/>
>  \- `postman`을 사용하면 API 요청을 쉽게 테스트해 볼 수 있습니다.<br/>
> <https://www.postman.com/>
{: .prompt-info }

<br/>

---

## Issue
- 문제 내용
  
```shell
json-server : 이 시스템에서 스크립트를 실행할 수 없으므로 C:\Users\devi\AppData\Roaming\npm\json-server.ps1 파일을 로드할 수 없습니다. 자세한 내용은 about_Execution_Policies(https://go.microsoft.com/fwlink/?LinkID=135170)를 참조하십시
오.
위치 줄:1 문자:1
+ json-server --watch ./src/db/data.json --port 3000
+ ~~~~~~~~~~~
    + CategoryInfo          : 보안 오류: (:) [], PSSecurityException
    + FullyQualifiedErrorId : UnauthorizedAccess
```

- 해결 방법
  - Windows - Windows PowerShell 관리자 권한 실행
  - 명령어 입력
    - `set-ExecutionPolicy RemoteSigned` - `Y`

![powershell](/assets/img/posts/web/etc/json_server/json_server_01.png)
_powershell_

 - 다시 실행

```shell
json-server --watch ./data.json --port 3000
```

![json-server start](/assets/img/posts/web/etc/json_server/json_server_02.png)
_json-server start_

 - 확인
   - localhost:3000/animals
  
![json-server test](/assets/img/posts/web/etc/json_server/json_server_03.png)
_json-server test_

<br/>

---

## 마무리

`json-server`에 대해서 정리하였습니다. 해당 내용 이외에도 더 많은 내용이 있기 때문에 필요하시면 `참고 자료`를 참조하시면 됩니다.


📑 **참고 자료**
- [json-server](https://www.npmjs.com/package/json-server)
- [HELOPY DEV](https://www.heropy.dev/p/zZdlXx)


<br/>
> 해당 글은 잘못되거나 새로운 내용이 확인되면 언제든 수정될 수 있습니다.
{: .prompt-info }
<br/>