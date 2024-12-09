---
title: CSS 선택자(Selector) 문법 정리
date: 2024-12-03 00:00:00 +09:00
description: CSS 선택자(Selector)에 대한 문법 정리
categories: [Web, Front-End]
tags: [Front-End, CSS]
hidden: false
image:
  path: /assets/img/logo/css_logo.png
  alt: css
---

## CSS 선택자(Selector)란?
`선택자(Selector)`는 스타일을 적용할 `HTML` 요소(Tag)를 지정할 때 사용됩니다. <br/>
`선택자(Selector)`는 기본적인 선택자 이외에 `결합 선택자`, `동위 선택자`, `의사 선택자` 등이 있으며 이러한 선택자에 대하여 정리하고자 합니다.<br/>
`CSS`에 대한 기본 적인 내용은 [여기](https://devistory.github.io/posts/css-basic/ "css-basic")를 참고하시기 바랍니다.

<br/>

---

## 결합 선택자(Combinator selector)
CSS는 하나 이상의 선택자를 사용할 수 있으며 `결합 선택자`는 선택자 간의 관계를 설정하여 사용합니다.
<br/>

### 자손 선택자(Descendant selector)
- `자손 선택자(Descendant selector)`는 `'A'`요소(element) 하위에 있는 모든 `'B'`요소(element)를 선택
- `A B` 처럼 요소(element) 사이에 `공백(single space)`을 사용

```html
<p>This is p inside div.</p>  
<div>
  <p>This is p inside div.</p>
  <span>
    <p>This is p inside div & span.</p>
  </span>
</div>
```

```css
div p {
  background-color : black;
  color : white;
}
```

![Descendant selector example result](/assets/img/posts/css/css_selector_01.png)
_Descendant selector example result_


<br/>

### 자식 선택자(Child selector)
- `자식 선택자(Child selector)`는 `'A'`요소(element) 바로 한 단계 하위(`자식`)에 있는 모든 `'B'`요소(element)를 선택
- `A > B` 처럼 요소(element) 사이에 `>`기호를 사용

```html
<p>This is p inside div.</p>  
<div>
  <p>This is p inside div.</p>
  <span>
    <p>This is p inside div & span.</p>
  </span>
</div>
```
```css
div > p {
  background-color : black;
  color : white;
}
```


![Child selector example result](/assets/img/posts/css/css_selector_02.png)
_Child selector example result_

<br/>

---

## 동위 선택자(Sibling selector)
`동위`는 **같은 위치 또는 등급** 을 의미하며, 같은 계층에서 동일한 `부모(Parents)` 요소(element)를 가진 `형제(Sibling)` 요소(element) 간에 관계를 설정하여 선택합니다.

### 일반 동위 선택자(General sibling selector)
- `일반 동위 선택자(General sibling selector)`는 `'A'`요소(element)와 동일 계층에 있는 모든 `'B'`요소(element)를 선택
- `A ~ B` 처럼 요소(element) 사이에 `~`기호를 사용

```html
<div>
  <h5>This is h5</h5>  
  <p>This is first p</p>
  <p>This is second p</p>
  <div>
    <p>This is third p</p>
  </div>
</div>
```

```css
h5 ~ p {
  background-color : black;
  color : white;
}
```

![General sibling selector example result](/assets/img/posts/css/css_selector_03.png)
_General sibling selector example result_

<br/>

### 인접 동위 선택자(Adjacent sibling selector)
- `인접 동위 선택자(Adjacent sibling selector)`는 `'A'`요소(element)와 동일 계층에서 바로 인접해 있는 `'B'`요소(element)를 하나 선택
- `A + B` 처럼 요소(element) 사이에 `+`기호를 사용

```html
<div>
  <h5>This is h5</h5>  
  <p>This is first p</p>
  <p>This is second p</p>
  <div>
    <p>This is third p</p>
  </div>
</div>
```

```css
h5 + p {
  background-color : black;
  color : white;
}
```

![Adjacent sibling selector example result](/assets/img/posts/css/css_selector_04.png)
_Adjacent sibling selector example result_

<br/>

---

## 의사 선택자(Pseudo selector)
일반적인 `선택자(Selector)`는 요소(element)를 직접 지정하여 선택하지만 `의사(가상) 선택자`는 요소(element)의 특정 `상태(state)` 또는 요소(element)의 `특정 부분`을 설정하여 선택합니다.

<br/>

### 의사 클래스(Pseudo classes)
- `의사 클래스(Pseudo classes)`는 요소(element)의 특별한 `상태(state)`를 기준으로 선택
- 다음과 같은 기준으로 선택 가능합니다.
  - 요소(element)에 마우스 오버(over), 클릭(click) 등
  - `link` 요소(element)의 방문 여부
  - 특정 요소(element)의 포커스(focus) 여부

<br/>

#### 동적 의사 클래스(Dynamic pseudo classes)
`동적 의사 클래스(Dynamic pseudo classes)`는 `링크(Link)`의 상태 별로 스타일을 설정할 수 있습니다.

| 선택자   | 설명                                                                                       |
| -------- | ------------------------------------------------------------------------------------------ |
| :link    | `링크(link)` 요소(element)를 한 번도 방문하지 않은 상태, 기본 상태                         |
| :visited | `링크(link)` 요소(element)를 한 번 이상 방문한 상태                                        |
| :hover   | 마우스 커서가 `링크(link)` 요소(element)에 올라간 상태                                     |
| :active  | 마우스를 `링크(link)` 요소(element)를 클릭하고 있는 상태                                   |
| :focus   | `링크(link)` 요소(element)가 키보드, 마우스 등의 조작으로 포커스(focus)를 가지고 있는 상태 |


```html
<div>
  <p><a hreaf="#">status : link</a></p>
  <p><a hreaf="#">status : visited</a></p>
  <p><a hreaf="#">status : hover</a></p>
</div>
```

```css
a:link {color: red;}
a:visited {color: blue;}
a:hover {color: orange;}
```



![Dynamic pseudo classes example result](/assets/img/posts/css/css_selector_05.png)
_Dynamic pseudo classes example result_


<br/>

#### 상태 의사 클래스(UI element states pseudo classes)
`상태 의사 클래스(UI element states pseudo classes)`는 `입력(input)` 요소(element)의 상태 별로 스타일을 설정할 수 있습니다.

| 선택자   | 설명                                                     |
| -------- | -------------------------------------------------------- |
| :checked | `입력(input)` 요소(element)가 체크된 상태                |
| :enabled | `입력(input)` 요소(element)가 활성화(사용 가능)된 상태   |
| :diabled | `입력(input)` 요소(element)가 비활성화(사용 불가)된 상태 |


```html
<div>
  <input type="checkbox" checked=true> 
    <span>check box</span>    
  </input><br/>
  <input type="checkbox">
    <span>check box</span>  
  </input>
</div>
```

```css
input:checked + span{
  color : red;
}
```
<style>
input:checked + span{
  color : red;
}
</style>


![Element states pseudo classes example result](/assets/img/posts/css/css_selector_06.png)
_Element states pseudo classes example result_

<br/>

#### 구조 의사 클래스(Structural pseudo classes)
`구조 의사 클래스(Structural pseudo classes)`는 계층 구조의 특정 위치에 대해서 스타일을 설정할 수 있습니다.

| 선택자            | 설명                                                                                                        |
| ----------------- | ----------------------------------------------------------------------------------------------------------- |
| :first-child      | 동일한 `부모(parents)` 요소(element)를 가진 `자식(child)`(=형제) 요소 중 첫 번째 요소                       |
| :last-child       | 동일한 `부모(parents)` 요소(element)를 가진 `자식(child)`(=형제) 요소 중 마지막 요소                        |
| :nth-child        | 동일한 `부모(parents)` 요소(element)를 가진 `자식(child)`(=형제) 요소 중 n번째 요소                         |
| :nth-last-child   | 동일한 `부모(parents)` 요소(element)를 가진 `자식(child)`(=형제) 요소 중 뒤에서 부터 n번째 요소             |
| :first-of-type    | 동일한 `부모(parents)` 요소(element)를 가진 특정 형식의 `자식(child)`(=형제) 요소 중 첫 번째 요소           |
| :last-of-type     | 동일한 `부모(parents)` 요소(element)를 가진 특정 형식의 `자식(child)`(=형제) 요소 중 마지막 요소            |
| :nth-of-type      | 동일한 `부모(parents)` 요소(element)를 가진 특정 형식의 `자식(child)`(=형제) 요소 중 n번째 요소             |
| :nth-last-of-type | 동일한 `부모(parents)` 요소(element)를 가진 특정 형식의 `자식(child)`(=형제) 요소 중 뒤에서 부터 n번째 요소 |
| :only-child       | 동일한 `부모(parents)` 요소(element)를 가진 `자식(child)`(=형제) 요소가 하나만 있는 요소                    |
| :only-of-type     | 동일한 `부모(parents)` 요소(element)를 가진 `자식(child)`(=형제) 요소중 특정 형식의 요소가 하나만 있는 요소 |
| :empty            | `자식(child)`(=형제) 요소가 없는 요소                                                                       |
| :root             | 문서의 `root` 요소                                                                                          |

- `first-child`, `last-child` Example

```html
<div>
  <p>A</p>
  <p>B</p>
  <p>C</p>
  <p>D</p>
  <p>E</p>
  <p>F</p>
</div>
```

```css
/* Exmpale을 위한 공통 내용 */
p{  
  width : 20px;
  height : 20px;
  text-align : center;
  display: inline-block;
}

/* 첫 번째 요소 */
p:first-child {
  background-color : red;
  color : white;
}

/* 마지막 요소 */
p:last-child {
  background-color : blue;
  color : white;
}
```


![Structural pseudo classes example result](/assets/img/posts/css/css_selector_07.png)
_Structural pseudo classes example result_

<br/>

- `nth-child`. `nth-last-child` Example

```css
/* n번째 요소 */
p:nth-child(2) {
  background-color : red;
  color : white;
}

/* 마지막 기준으로 n번째 요소 */
p:nth-last-child(2) {
  background-color : blue;
  color : white;
}
```


![Structural pseudo classes example result](/assets/img/posts/css/css_selector_08.png)
_Structural pseudo classes example result_

<br/>

```css
/* n간격 요소 : 2칸씩*/
p:nth-child(2n) {
  background-color : red;
  color : white;
}

/* n간격 요소 : 3칸씩*/
p:nth-child(3n) {
  background-color : orange;
  color : white;
}

/* n간격 요소 : 2칸씩, 시작 기준 첫 번째 요소*/
p:nth-child(2n+1) {
  background-color : green;
  color : white;
}

/* n간격 요소 : 3칸씩, 시작 기준 두 번째 요소*/
p:nth-child(3n+2) {
  background-color : purple;
  color : white;
}

/* n간격 요소 : 1칸씩, 시작 기준 세 번째 요소*/
p:nth-child(n+3) {
  background-color : blue;
  color : white;
}
```

![Structural pseudo classes example result](/assets/img/posts/css/css_selector_09.png)
_Structural pseudo classes example result_

<br/>

```css
/* 홀수 요소 */
p:nth-child(odd) {
  background-color : red;
  color : white;
}

/* 짝수 요소 */
p:nth-child(even) {
  background-color : blue;
  color : white;
}
```
![Structural pseudo classes example result](/assets/img/posts/css/css_selector_10.png)
_Structural pseudo classes example result_

<br/>

- `first-of-type`, `last-of-type` example

```html
<div>
  <text>A</text>
  <text>B</text>
  <p>C</p>
  <p>D</p>
  <text>E</text>
  <p>F</p>
</div>
```

```css
/* Exmpale을 위한 공통 내용 */
p, text{  
  width : 20px;
  height : 20px;
  text-align : center;
  display: inline-block;
}
/* 특정 형식의 첫 번째 요소 : p 요소의 첫 번째 요소*/
p:first-of-type {
  background-color : red;
  color : white;
}
/* 특정 형식의 마지막 요소 : text 요소의 마지막 요소 */
text:last-of-type {
  background-color : blue;
  color : white;
}
```

![Structural pseudo classes example result](/assets/img/posts/css/css_selector_11.png)
_Structural pseudo classes example result_

<br/>

- `nth-of-type`,`nth-last-of-type` Example

```css
/* 특정 형식의 n번째 요소 : p 요소의 두 번째 요소 */
p:nth-of-type(2) {
  background-color : red;
  color : white;
}

/* 특정 형식의 뒤에서 부터 n번째 요소 : text 요소의 뒤에서 부터 두 번째 요소 */
text:nth-last-of-type(2) {
  background-color : blue;
  color : white;
}
```


![Structural pseudo classes example result](/assets/img/posts/css/css_selector_12.png)
_Structural pseudo classes example result_


- `only-child`,`only-of-type` Example

```html
<div>
  <text>A</text>
</div>
<div>
  <p>A</p>
</div>
<div>
  <p>A</p>
  <text>B</text>
  <text>C</text>
</div>
<div>
  <p>A</p>
  <p>B</p>
  <text>C</text>
</div>
```
```css
/* 자식(=형제)요소 하나만 있는 요소 : 자식 요소가 하나만 있는 p요소 */
p:only-child {
  background-color : red;
  color : white;
}

/* 특정 형식 자식(=형제)요소 하나만 있는 요소 : text 요소가 하나인 요소 */
text:only-of-type {
  background-color : blue;
  color : white;
}
```

![Structural pseudo classes example result](/assets/img/posts/css/css_selector_13.png)
_Structural pseudo classes example result_

<br/>



### 의사 요소(Pseudo elements)
- `의사 요소(Pseudo elements)`는 요소(element)의 `특정 부분`을 기준으로 선택
- 다음과 같은 용도로 활용 가능합니다.
  - 요소의 첫 글자, 첫 줄 등
  - 요소 앞, 뒤에 콘텥츠 삽입
  - 목록 항목의 마커 스타일 지정

> **참고 사항**<br/>
> \- `의사 클래스(Pseudo classes)`는 `:`를 사용<br/> 
> \- `의사 요소(Pseudo elements)`는 `::`를 사용
{: .prompt-info }

  
|선택자|설명|
|::first-letter|특정 요소(element)의 `내용(content)` 첫 글자|
|::first-line|특정 요소(element)의 `내용(content)` 첫 줄|
|::before|특정 요소(element)의 `내용(content)` 이전 위치 선택, 새로운 `내용`을 삽입할 때 사용|
|::after|특정 요소(element)의 `내용(content)` 이후 위치 선택, 새로운 `내용`을 삽입할 때 사용|
|::selection|특정 요소(element)에서 사용자가 드래그(=mouse drag)한 `내용(content)`을 선택|

```html
<div>
  <p>
    Hello Wolrd<br/>
    This is Devistory
  </p>
  <text>This is example</text>
</div>
```

```css
p::first-letter{
  color: red;
}

p::first-line{
  font-style:italic;
}

text::before{
  content : ">> ";
}

text::after{
  content : "!!!";
  color : red;
}

p::selection{  
  color : white;
  background-color : purple;
}
```


![Pseudo elements example result](/assets/img/posts/css/css_selector_14.png)
_Pseudo elements example result_

<br/>

---

## 속성 선택자(Attribute selector)
`속성 선택자(Attribute selector)`는 특정 `속성(attribute)` 또는 `속성 값(attribute value)`을 기준으로 요소(element)를 선택하여 사용합니다.

| 선택자            | 설명                                                                                                                                       |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| [att]             | 요소(element)에 특정 `속성(attribute)`이 있으면 모두 선택                                                                                  |
| [att = "value"]   | 요소(element)에 특정 `속성(attribute)`이 있으며, `속성 값(attribute value)`이 일치하면 모두 선택                                           |
| [att ~="value"]   | 요소(element)에 특정 `속성(attribute)`이 있으며 문자열로 이루어진 `속성 값(attribute value)`에 설정한 문자가 있으면 모두 선택              |
| [att \|= "value"] | 요소(element)에 특정 `속성(attribute)`이 있으며 문자열로 이루어진 `속성 값(attribute value)`이 설정한 문자로 시작하는 문자열이면 모두 선택 |
| [att ^= "value"]  | 요소(element)에 특정 `속성(attribute)`이 있으며 `속성 값(attribute value)`으로 설정한 문자열로 시작하는 단어가 있으면 모두 선택            |
| [att $= "value"]  | 요소(element)에 특정 `속성(attribute)`이 있으며 `속성 값(attribute value)`으로 설정한 문자열로 끝나는 단어가 있으면 모두 선택              |
| [att *= "value"]  | 요소(element)에 특정 `속성(attribute)`이 있으며 `속성 값(attribute value)`으로 설정한 문자열을 포함하고 있으면 모두 선택                   |

> **주의**<br/>
>  `~=`는 띄어쓰기(space)로 구분된 단어 기준으로 판단<br/>
>  Ex) [title] ~= "abc" <br/> 
> \- title = "abc def" (O)<br/> 
> \- title = "abc-def" (X)
{: .prompt-warning }

<br/>

```html
<div>
  <h5 tag="">This is h5 (tag)</h5>
  <h5 title="abc">This is h5 (title : abc)</h5>
  <h5 title="abcdef">This is h5 (title : abcdef)</h5>
  <h6 title="x abc def">This is h6 (title : x abc def)</h6>
  <h6 title="x abc-def">This is h6 (title : x abc-def)</h6>
  <h6 title="abc-def">This is h6 (title : abc-def)</h6>
  <p title="abc def">This is p (title : abc def)</p>
  <p title="123-abc">This is p (title : 123-abc)</p>
</div>
```

```css
/* tag 속성이 포함된 요소 선택 */
[tag]{
  color: blue;
}

/* title 속성의 값이 "abc" 문자열이 있는 요소 선택 */
[title *= "abc"]{
  font-style: italic;
}

/* h5 요소중 title 속성의 값이 "abc" 문자열인 것 선택 */
h5[title = "abc"]{
  color: red;
}

/* h6 요소중 title 속성의 값이 "abc"가 포함된 문자열 요소 */
h6[title ~= "abc"]{
  color: green;
}

/* h6 요소중 title 속성의 값이 "abc"로 시작하는 문자조합 요소 */
h6[title |= "abc"]{
  color: orange;
}

/* p 요소중 title 속성의 값이 "abc"로 시작하는 요소 */
p[title ^= "abc"]{
  color: gray;
}

/* p 요소중 title 속성의 값이 "abc"로 끝나는 요소 */
p[title $= "abc"]{
  color: purple;
}
```


![Pseudo elements example result](/assets/img/posts/css/css_selector_15.png)
_Pseudo elements example result_

<br/>

---

## 마무리

`CSS`의 `선택자(Selector)` 문법에 대해서 정리하였습니다. 해당 내용 이외에도 더 많은 내용이 있기 때문에 필요하시면 `참고 자료`를 참조하시면 됩니다.

<br/>

📑 **참고 자료**
- <https://www.w3schools.com/css/default.asp>
- <https://www.tcpschool.com/css/intro>
- <https://inpa.tistory.com/entry/CSS-📚-선택자-문법-정리-심화#기본_선택자>

<br/>

> **Tip** <br/>
> `css`를 간단하게 사용해 보고 싶으시면 `CodePen`에서 연습해 볼 수 있습니다.<br/>
> [CodePen](https://codepen.io/mobify/pen/DRyBoB) 
{: .prompt-tip }


<br/>
> 해당 글은 잘못되거나 새로운 내용이 확인되면 언제든 수정될 수 있습니다.
{: .prompt-info }
<br/>