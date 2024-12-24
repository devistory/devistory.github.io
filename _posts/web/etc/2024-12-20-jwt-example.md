---
title: JWT (Json Web Token) 인증 예제
date: 2024-12-20 00:00:00 +09:00
description: JWT(Json Web Token) 인증 예제 코드
categories: [WEB, Etc]
tags: [JWT, Secrurity, Token,]
hidden: false
image:
  path: /assets/img/logo/jwt_logo.png
  alt: jwt
---

이 글은 `React`와 `Node.js`를 사용하여 `JWT(Json Web Token)`를 사용한 로그인 Example Code 입니다.

<br/>

---
## Example 구조
- Front-End : React
  - 화면 구성
    - /login : 로그인 form page
    - /main : 로그인 후 접근 가능한 page, (token 확인, logout button)

![login page](/assets/img/posts/web/etc/jwt_example/jwt_example_01.png)
_login page_
<br/>

![main page](/assets/img/posts/web/etc/jwt_example/jwt_example_02.png)
_main page_

- Back-End : Node.js  
  - Package
    - express
    - jsonwebtoken
    - body-parser
    - cookie-parser
    - cors

- 기타
  - 쿠키 보안을 위해서 `httpOnly`,`secure`,`sameSite` 등 추가
  - `refresh token rotation`으로 `refresh token`을 일회성으로 사용

<br/>

---
## Example
### Front-End(React)
#### App.js

```react
import {BrowserRouter, Route, Routes} from 'react-router-dom';
import './App.css';

import LoginPage from './page/login';
import MainPage from './page/main';

function App() {
  return (
    <BrowserRouter>
      <div className="App">
        <Routes>
          <Route path='/login' element={<LoginPage/>}/>
          <Route path='/' element={<MainPage/>}/>
        </Routes>
      </div>
    </BrowserRouter>
  );
}

export default App;
```
{: file="App.js" }


#### login page

```react
import React, { useState } from 'react';
import { BrowserRouter as Router, Routes, Route, useNavigate } from 'react-router-dom';
import axios from 'axios';

export default function LoginPage(){
    const backend_url = "http://localhost:4000";

    const [username, setUsername] = useState('');
    const [password, setPassword] = useState('');
    const navigate = useNavigate();
    
    const handleSubmit = async (e) => {
            e.preventDefault();
            try {
                const response = await axios.post(`${backend_url}/login`, {
                    username,
                    password,
                });
                localStorage.setItem('accessToken', response.data.accessToken);
                navigate('/', {replace: true});
            } catch (error) {
                console.log(error);
                alert('Login failed!');
            }
        };
    

    return(
        <div>
            <h1>Login</h1>
            <form onSubmit={handleSubmit}>
                <p>
                    <input
                        type="text"
                        placeholder="Username"
                        value={username}
                        onChange={(e) => setUsername(e.target.value)}
                    />
                </p>
                <p>
                    <input
                        type="password"
                        placeholder="Password"
                        value={password}
                        onChange={(e) => setPassword(e.target.value)}
                    />
                </p>
                <button type="submit">Login</button>
            </form>
        </div>
    );
}
```
{: file="login.jsx" }


![login page](/assets/img/posts/web/etc/jwt_example/jwt_example_01.png)
_login page_

<br/>

#### main page

```react
import axios from 'axios';
import { BrowserRouter as Router, Routes, Route, useNavigate } from 'react-router-dom';

axios.defaults.withCredentials = true; 

export default function MainPage(){
    const navigate = useNavigate();
    const backend_url = "http://localhost:4000";
    
    const handleVerify = async () => {
        let accessToken = localStorage.getItem('accessToken');
        try {
            const response = await axios.get(`${backend_url}/verify`, {
            headers: { Authorization: accessToken },
            });
            alert(response.data.message);
        } catch (error) {
            alert('Token is invalid or expired');
            await handleRefreshToken();
        }
    };

    const handleRefreshToken = async () => {
        try {
            const response = await axios.post(`${backend_url}/refresh`,{},{
            });
            localStorage.setItem('accessToken', response.data.accessToken);
            alert('Token refreshed! Please try again.');
        } catch (error) {
            alert('Failed to refresh token');
        }
    };


    const handleLogout = async () => {
        try {
        await axios.post(`${backend_url}/logout`);
        localStorage.removeItem('accessToken');
            navigate('/login');
            alert('Logged out successfully');
        } catch (error) {
            alert('Failed to logout');
        }
    };


    return(
        <div>
            <h1>Welcome to the Main Screen!</h1>
            <button onClick={handleVerify}>Verify Token</button>
            <button onClick={handleLogout}>Logout</button>
        </div>
    );
}
```
{: file="main.jsx" }


![main page](/assets/img/posts/web/etc/jwt_example/jwt_example_02.png)
_main page_

<br/>

### Back-End(Nodejs)
#### 기본 설정
- 사용할 package 및 기본 설정

```javascript
const express = require("express");
const jwt = require("jsonwebtoken");
const bodyParser = require("body-parser");
const cookieParser = require("cookie-parser");
const cors = require("cors");

const app = express();
const PORT = 4000;      // server 접근 port

// SECRET_KEY, REFRESH_SECRET_KEY는 사용자 임의의 값 사용, 길고 복잡할 수로 안전
const SECRET_KEY = "my_secret_key";
const REFRESH_SECRET_KEY = "my_refresh_secret_key";

// Middleware
app.use(bodyParser.json({ extended : false }));
app.use(cookieParser());
app.use(
    cors({
        origin: "http://localhost:3000",
        credentials: true,
    })
);

// Mock User Data
const users = [
  { id: 1, username: "tester", password: "1234" }
  ]; 

// In-memory store for refresh tokens
let refreshTokens = [];

//
// ... 기능 정의 code 생략 ...
//

app.listen(PORT, () =>
    console.log(`Server running on http://localhost:${PORT}`)
);
```
{: file="index.js" }

#### JWT Auth Function 정의
- JWT Auth(인증)에 필요한 Function 정의
  - generateAccessToken : accessToken 생성
  - generateRefreshToken : refreshToken 생성
  - verifyAccessToken : accessToken 확인
  - verifyRefreshToken : refreshToken 확인
  - removeRefreshToken : refreshToken 삭제

```javascript
const generateAccessToken = (payload) => {
    return jwt.sign(
        payload, 
        SECRET_KEY, 
        {
            algorithm: "HS256",
            expiresIn: "10m",
        }
    );
};

const generateRefreshToken = (payload) => {
    const refreshToken = jwt.sign(
        payload,
        REFRESH_SECRET_KEY,
        { 
            algorithm: "HS256",
            expiresIn: "1h", 
        }
    );
    refreshTokens.push(refreshToken);
    return refreshToken;
};

const verifyAccessToken = (token) => {
    return new Promise((resolve, reject) => {
        jwt.verify(token, SECRET_KEY, (err, decoded) => {
            if (err) reject(err);
            resolve(decoded);
        });
    });    
};

const verifyRefreshToken = (token) => {
    return new Promise((resolve, reject) => {
    jwt.verify(token, REFRESH_SECRET_KEY, (err, decoded) => {
            if (err) reject(err);
            resolve(decoded);
        });
    });
};

const removeRefreshToken = (oldToken) => {
    refreshTokens = refreshTokens.filter((token) => token !== oldToken);
};
```
{: file="index.js" }

#### route
- access method 정의
  - [POST] /login : 로그인
  - [POST] /logout : 로그아웃
  - [POST] /refresh : token 갱신
  - [GET] /verify : token 확인

```javascript
// Login Route
app.post("/login", (req, res) => {
    
    const { username, password } = req.body;
    const user = users.find(
        (u) => u.username === username && u.password === password
    );

    if (user) {
        const payload = { 
            id: user.id, 
            username: user.username 
        }
        const accessToken = generateAccessToken(payload);
        const refreshToken = generateRefreshToken(payload);

        res.cookie("refreshToken", refreshToken, {
            httpOnly: true,         // Javacript로 token 접근 금지
            secure: true,           // HTTPS 사용, 데이터 암호화
            sameSite: "strict",     // Domain 일치 검증
        });
        
        return res.json({ accessToken });
    } else {
        return res.status(401).json({ message: "Invalid credentials" });
    }
});

// Logout Route
app.post("/logout", (req, res) => {
    const refreshToken = req.cookies.refreshToken;

    if (refreshToken) {
        removeRefreshToken(refreshToken);
        res.clearCookie("refreshToken", {
            httpOnly: true,       // Javacript로 token 접근 금지
            secure: true,         // HTTPS 사용, 데이터 암호화
            sameSite: "strict",   // Domain 일치 검증
        });
    }

    return res.json({ message: "Logged out successfully" });
});

// Refresh Token Route
app.post("/refresh", async (req, res) => {
    const refreshToken = req.cookies.refreshToken;
    
    if (!refreshToken) {
        return res.status(401).json({ message: 'No refresh token provided' });
    }
    
    if (!refreshTokens.includes(refreshToken)) {
        return res.status(403).json({ message: 'Invalid refresh token' });
    }

    try {
      const decoded = await verifyRefreshToken(refreshToken);
      
      // Remove old refresh token and issue a new one
      const payload = {
              id : decoded.id,
              username : decoded.username,
          }
      removeRefreshToken(refreshToken);
      const newRefreshToken = generateRefreshToken(payload);
      
      res.cookie("refreshToken", newRefreshToken, {
          httpOnly: true,
          secure: false, // Set to true in production with HTTPS
          sameSite: "strict",
      });

      const newToken = generateAccessToken(payload);
      return res.json({ accessToken: newToken });
    } 
    catch (err) {
      return res
      .status(403)
      .json({ message: "Failed to authenticate refresh token" });
    }
});

// Verify Token Route
app.get("/verify", async (req, res) => {
    const accessToken = req.headers["authorization"];

    if (!accessToken) {
      return res.status(403).json({ message: "No token provided" });
    }

    try {
      const decoded = await verifyAccessToken(accessToken);
      return res.json({ message: "Token is valid ", user: decoded.username });
    } 
    catch (err) {
      return res.status(403).json({ message: "Failed to authenticate token" });
    }
});

```
{: file="index.js" }

<br/>

---
## 마무리

`JWT(Json web Token)`를 이용한 로그인 페이지 Example code 입니다. 해당 Example은 `참고 자료`의 내용을 기반으로 작성하였습니다. `JWT(Json web Token)`에 대한 내용이 궁금하시다면 [여기](https://devistory.github.io/posts/jwt/ "jwt") 또는 `참고 자료`를 참조하시면 됩니다.

<br/>

📑 **참고 자료**
- [코딩애플(JWT 대충 쓰면 님들 코딩인생 끝남)](https://youtu.be/XXseiON9CV0?si=enjUMw_pzPW2_uwe)
- [얄팍한 코딩사전(세션 VS. 토큰! JWT가 뭔가요?)](https://youtu.be/1QiOXWEbqYQ?si=DqXRD4xYsexr6CPH)
- [Inpa Dev 블로그](https://inpa.tistory.com/entry/WEB-📚-JWTjson-web-token-란-💯-정리#token_방식의_단점)
- [jwt.io](https://jwt.io/)

<br/>

> **Tip** <br/>
> `JWT`를 간단하게 만들어 보고 싶으시면 `jwt.io`에서 만들어 볼 수 있습니다.<br/>
> [jwt.io](https://jwt.io/) 
{: .prompt-tip }


<br/>
> 해당 글은 잘못되거나 새로운 내용이 확인되면 언제든 수정될 수 있습니다.
{: .prompt-info }
<br/>


