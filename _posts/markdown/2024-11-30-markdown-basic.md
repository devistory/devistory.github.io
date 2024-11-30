---
title: Markdown 기본 문법
date: 2024-11-29 00:00:00 +09:00
description: Markdown을 사용하기 위한 기본 문법 정리
categories: [Markdown]
tags: [Markdown]
hidden: false
image:
  path: /assets/img/logo/markdown_logo.png
  alt: GitHub
---

이 글은 .md파일을 작성하기 위한 기본적인 `Markdown` 문법에 대하여 정리하고자 합니다.

## 마크다운(Markdown)이란?
마크다운(Markdown)은 간단하고 읽기 쉬운 텍스트 기반의 마크업 언어입니다. 개발자들이 코드 문서화나 블로그 작성에 널리 사용하는데, 작성 문법이 직관적이고 간결하기 때문입니다

- 간단한 문법: 기본적인 텍스트로 서식을 지정할 수 있습니다.
- 가독성: 마크다운 문서 자체가 읽기 쉬우며 HTML 등으로 변환했을 때도 깔끔합니다.
- 플랫폼 호환성: 다양한 도구와 플랫폼에서 지원합니다(예: GitHub, Notion, VS Code 등).
- 경량 언어: 마크업 언어 중에서도 매우 가벼워서 학습하기 쉽습니다.

<br>

---

## 제목 (Headers)
- #으로 시작하는 텍스트 입력
- #의 개수가 많아 질수록 크기가 작아짐
- #은 1~6개까지 사용 가능
- \-기호 전 라인에 텍스트 입력


```markdown
# H1 제목
## H2 제목
### H3 제목
#### H4 제목
##### H5 제목
###### H6 제목

Hyphen(-)으로 제목표현
-
```



![Headers Example results](/assets/img/posts/markdown/markdown_01.png)
_Headers Example results_


<br>

---


## 목록 (Lists)
### 순서가 있는 목록 (Ordered lists)
- 숫자로 시작하는 텍스트 입력
- 들여쓰기(띄어쓰기 3번), List 안에 List 생성 (Depth 추가)

```markdown
1. 1 Depth 목록
1. 1 Depth 목록
    1.  2 Depth 목록
    1.  2 Depth 목록
1. 1 Depth 목록
    1. 2 Depth 목록
        1. 3 Depth 목록
        1. 3 Depth 목록
```

![Ordered Lists Example results](/assets/img/posts/markdown/markdown_02.png)
_Ordered Lists Example results_
  
   
<br>

   
### 순서가 없는 목록 (Unordered lists)
- -, *, +로 시작하는 텍스트 입력
- 들여쓰기(띄어쓰기 2번), List 안에 List 생성 (Depth 추가)
  
```markdown
- 과일
  - 사과
  - 바나나
  
- 동물
  - 강아지
  - 고양이
  
- 1 Depth 목록
  - 2 Depth 목록
    - 3 Depth 목록
      - 4 Depth 목록
```


![Unordered Lists Example results](/assets/img/posts/markdown/markdown_03.png)
_Unordered Lists Example results_


<br>

### 체크박스 목록 (CheckBox lists)
- -, *, +로 시작하는 텍스트 입력 후에 `[ ]`대괄호 사용
- `[ ]` 빈 체크박스
- `[x]` 체크된 체크박스
	\* `[ ]` 사용할때 가운데 띄어쓰기 필수
 	\* x는 대소문자 구분 없음

```markdown
- [ ] 빈 박스
- [x] 체크된 박스
- [X] 체크된 박스
```

![CheckBox Lists Example results](/assets/img/posts/markdown/markdown_04.png)
_CheckBox Lists Example results_

<br>

---

## 표 (Table)
- header와 cell을 구분하기 위해서는 - 기호(Hyphen) 3개 필요(---)
- cell 정렬을 위해서는 : 기호(Colns) 사용
  - Left ( :--- )	* 정렬 지정이 없을 경우 Left가 기본값
  - Center ( :---: )
  - Right ( ---: )

```markdown
| header1 | header2 | header3 |
| ------- | ------- | ------- |
| AAA     | BBB     | CCC     |
| DDD     | EEE     | FFF     |
| GGG     | HHH     | III     |
```

![Table Lists Example results](/assets/img/posts/markdown/markdown_05.png)
_Table Example results_

<br>

```markdown
| header1 | header2 | header3 |
| :------ | :-----: | ------: |
| AAA     |   BBB   |     CCC |
| DDD     |   EEE   |     FFF |
| GGG     |   HHH   |     III |
```


![Table Example results](/assets/img/posts/markdown/markdown_06.png)
_Table Example results_


> 참고사항<br/>
> \- Velog에서는 table 정렬이 적용 안됨
{: .prompt-info }


<br>

---
## 강조 (Emphasis)
- 기울이기(italic) : 텍스트 양끝에 * 또는 _ 사용
- 두껍게(bold) : 텍스트 양끝에 ** 또는 __ 사용
- 가운데 줄 : 텍스트 양끝에 ~~ 사용
- 밑줄 : markdown에서 밑줄은 지원하지 않기 때문에 <u>텍스트</u> 사용
- 중첩해서 사용

```markdown
*기울어진 텍스트 입니다.*
_기울어진 텍스트 입니다._

**두꺼운 텍스트 입니다.**
__두꺼운 텍스트 입니다.__

__*기울어지고 두꺼운 텍스트입니다.*__
~~*기울어지고 가운데 줄이 있는 텍스트입니다.*~~

~~가운데 줄이 있는 텍스트 입니다.~~
<u>밑줄이 있는 텍스트 입니다.</u>
```


![Emphasis Example results](/assets/img/posts/markdown/markdown_07.png)
_Emphasis Example results_


<br>

---

## 코드블럭 (CodeBlock)
- 한줄 코드블럭 : tab 이후 텍스트 작성
- 여러줄 코드블럭 : ` 기호(backtick) 3개로 텍스트 감싸기
	- 코드블럭 시작 부분 뒤에 언어를 지정해주면 syntax color 적용

```markdown
(tab) 한줄 코드 블럭

```javascript        <!--(`기호 3개,지정언어, 코드블럭 시작)-->
    function test(){
    	console.log("여러줄 코드 블럭");
    }
```     <!--(`기호 3개, 코드블럭 마무리)-->
```
 

![CodeBlock Example results](/assets/img/posts/markdown/markdown_08.png)
_CodeBlock Example results_


<br>

---
## 인용문 (BlockQuote)
- \> 기호로 시작하는 텍스트 입력
- \> 기호 여러개 사용하면 중첩 가능

```markdown
> 인용문 입니다.

>>인용문 입니다.

>>>인용문 입니다.
```

![BlockQuote Example results](/assets/img/posts/markdown/markdown_09.png)
_BlockQuote Example results_


<br>

---

## 링크 (Links)
### 외부 링크 (External Link)
- 외부 정보를 연결할 수 있는 텍스트
- \[화면에 표현될 텍스트](link주소 "Link 설명")
- <link주소>
	* <>기호 없어도 주소 형식 텍스트 사용시 자동 link
  
```markdown
구글 : [Google](http://www.google.com "구글")
다음 : [Daum](https://daum.net)
네이버 : <http://www.naver.com>
```

>
구글 : [Google](http://www.google.com "구글")
다음 : [Daum](https://daum.net)
네이버 : <http://www.naver.com>

<br/>

### 내부 링크 (Internal Link)
- 내부 제목(Header)로 연결할 수 있는 텍스트
- \[화면에 표현될 텍스트](\#헤더이름)
	* 헤더이름에서 띄어쓰기는 -기호로 대체, 영문은 소문자로 작성
- 소괄호, 이모지는 제거하고 작성

```markdown
[1. 제목 (Headers)](#제목-headers)
[2. 목록 (Lists)](#목록-lists)
```

>
[1. 제목 (Headers)](#제목-headers)<br/>
[2. 목록 (Lists)](#목록-lists)


<br>

---

## 이미지 (Images)
- 링크와 비슷하지만 앞에 !기호 사용
- \!\[텍스트\](이미지 주소 "설명")
- 이미지에 링크 추가
  - \[ \! \[텍스트] (이미지 주소) ] (Link 주소)
- 이미지 사이즈 수정
  - ``<img></img>`` 태그 사용

```markdown
![깃허브](https://velog.velcdn.com/images/devi/post/d59f0e52-e2cf-4d93-a629-719903750c28/image.png "github-logo")

[![구글](https://velog.velcdn.com/images/devi/post/def6fcce-f8f5-49a3-a530-fb9b5abf4f21/image.png)](https://google.com/)
```


![깃허브](/assets/img/github_logo.png "github-logo")
_GitHub Image Example results_

[![구글](/assets/img/google_logo.png)](https://google.com/)

<br/>

```html
<img src=/assets/img/github_logo.png" width=100px height=100px alt="github-logo"/>

<img src="/assets/img/google_logo.png" width=100px height=100px alt="google-logo"/>
```



<img src="/assets/img/github_logo.png" width=100px height=100px alt="github-logo"/>
_GitHub Image Example results_

<img src="/assets/img/google_logo.png" width=100px height=100px alt="google-logo"/>
_Google Image Example results_

<br>

---
## 이모지 (Emoji)
- 직접 복사, 붙여넣기
  - https://getemoji.com/
  
- 단축키
  - Windows : window key + .(마침표)
  - Mac : Command + Control + Space bar

❤️⭐🚀🍏🔷👻💩💀


<br>

---
## 수평선 (Horizontal Rule)
- 3가지 기호( \-, *, _ ) 중 한가지를 3개 이상 입력
	\* 수평선 사용시에 바로 이전 라인은 비워두어야 합니다. Header로 인식 할 수 있음

``` markdown
---
***
___
-----------
```

![Horizontal Example results](/assets/img/posts/markdown/markdown_10.png)
_Horizontal Example results_


<br>

---


## 주석 (Comment)
- `<!-- -->` 텍스트 감싸기
- `[//]: #`으로 텍스트 시작, 3가지 기호( ' ', " ", ( ) ) 중 한가지로 텍스트 감싸기

```markdown
주석(Comment) Example [start]
<!-- 주석 입니다. -->

[//]: # '주석입니다.'
[//]: # "주석입니다."
[//]: # (주석입니다.)

주석(Comment) Example [end]
```

![Comment Example results](/assets/img/posts/markdown/markdown_11.png)
_Comment Example results_

<br>

---
## 줄바꿈 (Line Breaks)
- `<br>`태그를 사용하여 줄바꿈

```markdown
“애초에 디버깅은 코드를 작성하는 것 보다 배나 힘들다. <br>그러니, 코드를 최대한 꼼꼼하게 작성하는 사람은, 당연히, 디버그할 정도로 똑똑하지 않은 것이다.”
“Debugging is twice as hard as writing the code in the first place. Therefore, if you write the code as cleverly as possible, you are, by definition, not smart enough to debug it.”<br><br> - 브라이언 커니핸(Brian W. Kernighan)

```

![Line Breaks Example results](/assets/img/posts/markdown/markdown_12.png)
_Line Breaks Example results_

## 마무리
`GitHub Page`에 글을 쓰기 위해서 `Markdown`을 정리하였습니다. `Markdown`은 `GitHub Page` 이외에 Project의 Readme 파일 등을 작성할 때도 사용되니 다양하게 활용할 수 있을 것 같습니다.



<br/>
> 해당 글은 틀린 내용 및 새로운 내용이 확인되면 언제든 수정될 수 있습니다.
{: .prompt-info }
<br/>


