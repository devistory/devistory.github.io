---
title: TanStack Query (React Query)
date: 2025-01-06 00:00:00 +09:00
description: TanStack Query 내용 정리
categories: [Web, React]
tags: [Front-End, React, TanStack Query]
hidden: false
image:
  path: /assets/img/logo/tanstack_logo.png
  alt: TanStack Query
---


## TanStack Query란?
`TanStack Query`(이전 명칭: React Query)는 React 애플리케이션에서 서버 상태(server state)를 관리하는 데 특화된 라이브러리입니다. 데이터 페칭, 캐싱, 동기화, 업데이트를 간편하고 효율적으로 처리할 수 있도록 설계되었습니다. React의 상태 관리 라이브러리로 Redux, MobX와 같은 것들이 있지만, TanStack Query는 서버와의 데이터 상호작용을 중점적으로 다룹니다.

### 대표 기능
 - **비동기 데이터 관리를 단순화** : 로딩, 에러, 성공 상태의 수동 관리를 제거합니다.
 - **최적화된 캐싱** : 쿼리 결과를 자동으로 캐싱하고 오래된 데이터를 지능적으로 무효화합니다.
 - **내장된 재시도 로직** : 실패한 요청을 자동으로 재시도하며 로직을 사용자 정의할 수 있습니다.
 - **반응성** : 데이터 변경 시 UI를 자동으로 업데이트합니다.
 - **백그라운드 업데이트** : 백그라운드에서 데이터를 새로 고쳐 매끄러운 사용자 경험을 제공합니다.
 - **개발자 도구 지원**: 쿼리를 검사할 수 있는 강력한 개발자 도구를 제공합니다.

### 데이터 캐싱 & 신선도

#### 데이터 캐싱
- `TanStack Query`는 쿼리를 통해 가져온 데이터를 캐싱하여 동일한 데이터 요청에 대해 서버 호출을 줄입니다.<br/>
- 캐싱된 데이터는 애플리케이션 내에서 즉시 재사용될 수 있어 빠른 응답성을 제공합니다.<br/>
- 각 쿼리는 고유한 **쿼리 키(Query Key)**를 기반으로 캐싱됩니다.<br/>
- 캐시된 데이터는 메모리에 저장되며, 특정 조건에서 유효성을 무효화하거나 새로 고칠 수 있습니다.

![Caching miss, hit](/assets/img/posts/web/react/tanstack_query/tanstack_query_01.png)
_Caching miss, hit_

<br/>

#### 데이터 신선도
 - `TanStack Query`는 캐싱한 데이터를 `신선한(Fresh)`, `상한(Stale)` 상태로 구분하여 관리합니다.
 - `staleTime` : 데이터를 신선하다고 간주하는 기간을 정의합니다. 이 기간 동안에는 추가 서버 요청 없이 캐시된 데이터가 사용됩니다.<br/>
기본값은 0으로, 가져온 데이터는 즉시 오래된 것으로 간주됩니다.
- `gcTime`: 오래된 데이터를 캐시에 유지하는 시간을 정의합니다. 해당 시간이 지나면 캐시가 삭제됩니다.<br/>
- `refetchOnWindowFocus`: 사용자가 브라우저 탭으로 다시 돌아오면 데이터를 새로 고칩니다(기본값: true).
- `refetchInterval`: 특정 간격으로 데이터를 주기적으로 새로 고칩니다.
- 백그라운드 새로고침: 데이터가 오래된 경우 백그라운드에서 데이터를 자동으로 새로고칩니다.

<br/>

![Fresh, Stale](/assets/img/posts/web/react/tanstack_query/tanstack_query_02.png)
_Fresh, Stale_

<br/>

---

## 설치
- tanstak query 설치 및 devtools 설치
```shell
npm install @tanstack/react-query @tanstack/react-query-devtools
```

<br/>

---

## queryClient
`TannStack Query`에서 가장 중요한 객체로, 모든 쿼리 관련 상태를 관리합니다.
`QueryClientProvider`를 통해 React 컴포넌트 트리에 전달되며, 전역적으로 쿼리 기능을 활성화합니다.

```react
import { QueryClient, QueryClientProvider } from '@tanstack/react-query';
import { ReactQueryDevtools } from '@tanstack/react-query-devtools'

const queryClient = new QueryClient();

function App() {
    return (
        <QueryClientProvider client={queryClient}>
            <YourComponent />
            <ReactQueryDevtools />  <!-- 선택사항 -->
        </QueryClientProvider>
    );
}
```
{: file="App.js" }

<br/>

---

## useQuery
`useQuery`는 데이터를 가져오는 데 사용됩니다. 주로 `GET` 요청에 사용되며, 캐싱, 자동 리패칭, 로딩/에러 상태 관리 등 여러 유용한 기능을 제공합니다.

```react
import { useQuery } from '@tanstack/react-query';
import axios from 'axios';

const fetchTodos = async () => {
  const { data } = await axios.get('/api/todos');
  return data;
};

function TodoList() {
  const {data, isLoading, isStale} = useQuery({
        queryKey : ["todo"],             // query를 식별할 고유값, 배열로 작성
        queryFn : fetchTodos,            // 동작 function
        staleTime : 60 * 1000,           // 데이터가 1분 동안 신선하다고 간주됨, default : 0
        gcTime : 60 * 1000 * 2,          // 데이터가 2분 동안 캐시에 유지됨
        
    })

  if (isLoading) return <div>Loading...</div>;
  if (error) return <div>Error: {error.message}</div>;

  return (
    <ul>
      {data.map((todo) => (
        <li key={todo.id}>{todo.title}</li>
      ))}
    </ul>
  );
}
```
{: file="fetchTodos.js" }

<br/>


> **참고 사항** <br/>
> `useQuery`의 options은 [여기](https://tanstack.com/query/latest/docs/framework/react/reference/useQuery "tanstack-query")를 참고하시기 바랍니다.
>
{: .prompt-info }

<br/>

---

## useMutation
`useMutation`은 데이터 변이에 사용됩니다. 주로 `POST`, `PUT`, `DELETE` 요청에 사용되며, 서버에 데이터를 업데이트하거나 추가, 삭제할 때 활용됩니다.

```react
import React from 'react';
import { useQuery, useMutation, useQueryClient } from '@tanstack/react-query';
import axios from 'axios';

// 데이터 가져오기 함수
const fetchTodos = async () => {
  const response = await axios.get('/api/todos');
  return response.data;
};

// 데이터 추가 함수
const addTodo = async (newTodo) => {
  const response = await axios.post('/api/todos', newTodo);
  return response.data;
};

function TodoApp() {
  const queryClient = useQueryClient();

  // useQuery로 Todo 리스트 가져오기
  const { data: todos, isLoading, error } = useQuery({
    queryKey: ['todos'], // 쿼리 키
    queryFn: fetchTodos, // 쿼리 함수
  });

  // useMutation으로 Todo 추가
  const mutation = useMutation({
    mutationFn: addTodo, // 변이 함수
    onSuccess: () => {
      queryClient.invalidateQueries({ queryKey: ['todos'] }); // 쿼리 무효화
    },
  });

  const handleAddTodo = (e) => {
    e.preventDefault();
    const title = e.target.elements.title.value;
    mutation.mutate({ title }); // 새로운 Todo 추가 요청
    e.target.reset();
  };

  if (isLoading) return <div>Loading...</div>;
  if (error) return <div>Error: {error.message}</div>;

  return (
    <div>
      <h1>Todo List</h1>
      <form onSubmit={handleAddTodo}>
        <input type="text" name="title" placeholder="Add a new todo" required />
        <button type="submit">Add</button>
      </form>
      <ul>
        {todos.map((todo) => (
          <li key={todo.id}>{todo.title}</li>
        ))}
      </ul>
    </div>
  );
}

export default TodoApp;
```
{: file="TodoApp.js" }

<br/>

> **참고 사항** <br/>
> `useMutation`의 options은 [여기](https://tanstack.com/query/latest/docs/framework/react/reference/useMutation "tanstack-query")를 참고하시기 바랍니다.
>
{: .prompt-info }

<br/>

---

## Example

> **참고 사항** <br/>
> \- Example은 `@tanstack/react-query 5.62.10` 기준으로 작성 되었습니다.<br/>
> \- Example에서의 RestAPI server는 `json server`를 사용하였습니다.<br/>
> `json server`에 대한 내용은 [여기](https://devistory.github.io/posts/json-server/ "json-server")를 참고하시기 바랍니다.
{: .prompt-info }

<br/>

> **주의 사항** <br/>
> Example Code에서 `CSS` 내용을 생략 하였습니다.
{: .prompt-warning }

<br/>

### useQuery,useMutation(Read, Creat, Update, Delete) Example
- `useQuery`,`useMutation`를 사용한 기본적인 사용 Example입니다.
- `useQuery`를 사용하여 data `Get` 처리(목록 가져오기)
- `useMutation`를 사용하여 data `Post`, `Put`, `Delete` 처리(생성,수정,삭제)

#### Example Code
```react
import './App.css';
import { QueryClient, QueryClientProvider } from "@tanstack/react-query";
import { ReactQueryDevtools } from '@tanstack/react-query-devtools'
import PostList from './PostList';

// Query Client 생성
const queryClient = new QueryClient();

function App() {
  return (
    <QueryClientProvider client={queryClient}>
      <div className="App">
        <h1>TanStack Example</h1>
        <PostList/>
        </div>  
      <ReactQueryDevtools />
    </QueryClientProvider>
  );
}

export default App;
```
{: file="App.js" }

<br/>

```react
import React from "react";
import { useQuery, useMutation, useQueryClient } from "@tanstack/react-query";
import { useState } from "react";
import axios from "axios";
import "./PostList.css"

// 데이터 가져오는 함수
const fetchPosts = async () => {
    const response = await axios.get("http://localhost:4000/posts");
    return response.data;
};

const addPost = async (newPost) => {
    const response = await axios.post("http://localhost:4000/posts", newPost);
    return response.data;
};

const updatePost = async (updatedPost) => {
    const response = await axios.put(
        `http://localhost:4000/posts/${updatedPost.id}`,
        updatedPost
    );
    return response.data;
};

const deletePost = async (postId) => {
    await axios.delete(`http://localhost:4000/posts/${postId}`);
};

const PostList = () => {
    console.log("PostList");
    const queryClient = useQueryClient();
    const [newPost, setNewPost] = useState({ title: "", content: "" });

    const { data, isLoading, isError, error } = useQuery({
        queryKey: ["posts"], 
        queryFn: fetchPosts
    });

    // Add post mutation
    const addPostMutation = useMutation({
        mutationFn: addPost,
        onSuccess: () => {
            queryClient.invalidateQueries(["posts"]);
        },
    });

    // Update post mutation
    const updatePostMutation = useMutation({
        mutationFn: updatePost,
        onSuccess: () => {
            queryClient.invalidateQueries(["posts"]);
        },
    });

    // Delete post mutation
    const deletePostMutation = useMutation({
        mutationFn: deletePost,
        onSuccess: () => {
            queryClient.invalidateQueries(["posts"]);
        },
    });

    if (isLoading) {
        return <div>Loading...</div>;
    }

    if (isError) {
        return <div>Error: {error.message}</div>;
    }

    const handleAddPost = () => {
        if (newPost.title && newPost.content) {
            addPostMutation.mutate(newPost);
            setNewPost({ title: "", content: "" });
        }
    };

    const handleUpdatePost = (post) => {
        const updatedPost = {
            ...post,
            title: `${post.title} (Updated)`,
        };
        updatePostMutation.mutate(updatedPost);
    };

    const handleDeletePost = (postId) => {
        deletePostMutation.mutate(postId);
    };

return (
    <div className="conainer">
        <div className="inputPanel">
            <h3>Add New Post</h3>
            <input
                type="text"
                placeholder="Title"
                value={newPost.title}
                onChange={(e) => setNewPost({ ...newPost, title: e.target.value })}
            />
            <textarea
                placeholder="Content"
                value={newPost.content}
                onChange={(e) => setNewPost({ ...newPost, content: e.target.value })}
            />
            <button onClick={handleAddPost}>Add Post</button>
        </div>
        <div className="listPanel">
                {data.map((post) => (
                    <div key={post.id} className="listItem">
                        <h3>{post.title}</h3>
                        <p>{post.content}</p>
                        <button onClick={() => handleUpdatePost(post)}>Update</button>
                        <button onClick={() => handleDeletePost(post.id)}>Delete</button>
                    </div>
                ))}
        </div>
    </div>
    );
};
export default PostList;
```
{: file="PostList.jsx" }

#### Example Result
- `json server`에 있는 *post 1~3* data `Get` 요청 후, 출력
- *post 4*에 대한 새로운 data `Post` 요청,
- *post 4* data `Delete` 요청
- *post 1~3* data `Update` 요청
  
<br/>

![useQuery,useMutation example](/assets/img/posts/web/react/tanstack_query/tanstack_query_02.gif)
_useQuery,useMutation example_

<br/>

### Caching Example
- 요청 Data의 상태 변화에 대한 Example입니다.
- `staleTime`을 5초로 설정하여 `신선한(Fresh)` 상태 유지
- `refetchInterval`을 10초로 설정하여 Data 갱신
  
#### Example Code
```react
import './App.css';
import { QueryClient, QueryClientProvider } from "@tanstack/react-query";
import { ReactQueryDevtools } from '@tanstack/react-query-devtools'
import FetchData from './caching';

// Query Client 생성
const queryClient = new QueryClient();

function App() {
  return (
    <QueryClientProvider client={queryClient}>
      <div className="App">
        <h1>TanStack Example</h1>
        <FetchData/>
        </div>  
      <ReactQueryDevtools />
    </QueryClientProvider>
  );
}

export default App;
```
{: file="App.js" }

<br/>

```react
import { useQuery } from '@tanstack/react-query';
import axios from 'axios';
import { useState, useEffect } from 'react';

async function GetPosts() {
    const response = await axios.get('http://localhost:4000/posts');
        return response.data;
}

export default function FetchData() {
    const [seconds, setSeconds] = useState(0);

    useEffect(() => {
        const interval = setInterval(() => {
        setSeconds((prev) => prev + 1);
        }, 1000);

        // 컴포넌트가 언마운트될 때 타이머 정리
        return () => clearInterval(interval);
    }, []);
    

    const {data, isLoading, isStale} = useQuery({
        queryKey :"data",
        queryFn : GetPosts,
        staleTime : 5 * 1000,           // 데이터가 5초 동안 신선하다고 간주됨, default : 0
        gcTime : 60 * 1000,             // 데이터가 1분동안 캐시에 유지됨
        refetchInterval : 10 * 1000     // 데이터를 10초 간격으로 갱신
        
    })

    if (isLoading) return <p>로딩 중...</p>;

    return (
        <div>
        <p>{seconds} seconds</p>
        <p>데이터: {JSON.stringify(data)}</p>
        <p>데이터가 신선한 상태: {isStale ? '아니오' : '예'}</p>
        </div>
    );
}
```
{: file="Caching.jsx" }

#### Example Result
- 5초 후, 'isStale`이 `stale`상태로 변경됨
  - '데이터가 신선한 상태: 아니오'로 변경
  - DevTools 우측 상단 `fresh` -> `stale`상태로 변경
- 10초 후, Data 갱신
  - 데이터의 `title`, `content` 내용이 변경

<br/>

![staleTime,refetch example](/assets/img/posts/web/react/tanstack_query/tanstack_query_01.gif)
_staleTime,refetch example_

<br/>


## 마무리

`tanstack-query`에 대해서 정리하였습니다. 해당 내용 이외에도 더 많은 내용이 있기 때문에 필요하시면 `참고 자료`를 참조하시면 됩니다.

<br/>

📑 **참고 자료**
- [Tanstack](https://tanstack.com/query/latest)
- [kakao pay tech](https://tech.kakaopay.com/post/react-query-1/#react-query-소개)
- [HELOPY DEV](https://www.heropy.dev/p/HZaKIE)

<br/>


> 🔖 **이미지 출처**<br/>
> Icons made by various authors from [www.flaticon.com](https://www.flaticon.com)
> - Icon made by Flat Icons from www.flaticon.com
> - Icon made by Vectorsclub from www.flaticon.com
> - Icon made by Uniconlabs from www.flaticon.com
> - Icon made by Umeicon from www.flaticon.com
> 
>*Thanks to the creators who created these great icons.*

<br/>
> 해당 글은 잘못되거나 새로운 내용이 확인되면 언제든 수정될 수 있습니다.
{: .prompt-info }
<br/>