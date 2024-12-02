---
title: Markdown (with:chirpy theme)
date: 2024-11-29 00:00:00 +09:00
description: chirpy theme에서 사용되는 Markdown 정리
categories: [Markdown]
tags: [Markdown, Chirpy]
hidden: false
image:
  path: /assets/img/logo/markdown_logo.png
  alt: Markdown
---

이 글은 `jekyll`의 `chirpy` Theme에서 사용되는 `Markdown`에 대하여 정리하고자 합니다. <br/>
`Markdown`에 대한 기본 문법은 [여기](https://devistory.github.io/posts/markdown-basic/ "markdown-basic")를 참고하시기 바랍니다.

<br>

---

## 이미지 (Iamges)
### 캔셥 (Caption)
- `chirpy`에서는 이미지 등록 내용 하단에 italic(이텔릭체)을 추가하면 capthon되어 이미지 하단에 나타납니다.

```markdown
![_GitHub](/assets/img/github_logo.png "github-logo")
_Image Caption Example results_
```

![GitHub](/assets/img/github_logo.png "github-logo")
_Image Caption Example results_

<br/>

### 크기 (Size)
 - `chirpy`에서는 이미지 크기를 조절하기 위해서 이미지 등록 내용 뒤에 `{: width="" height="" }`을 사용합니다.

```markdown
![GitHub](/assets/img/github_logo.png "github-logo"){: width="100" height="100" }
```

![GitHub](/assets/img/github_logo.png "github-logo"){: width="100" height="100" }
_Image resizing Example results_


> 참고사항<br/>
> \- `chirpy` ver 5.0.0 이상부터는 약어를 지원합니다.<br/>
> \- `width` : `w`<br/>
> \- `height` : `h`
> ```markdown
> ![GitHub](/assets/img/github_logo.png "github-logo"){: w="100" h="100" }
> ```
{: .prompt-info }

<br/>

### 위치 (Position)
- 이미지는 기본적으로 가운데에 배치되지만 `.normal`, `.left`, `.right`를 사용하면 위치를 지정할 수 있습니다.

```markdown
![GitHub](/assets/img/github_logo.png "github-logo"){: width="100" height="100" .normal }
이미지 `.normal` 입니다.
```
![GitHub](/assets/img/github_logo.png "github-logo"){: width="100" height="100" .normal }
이미지 `.normal` 입니다.

<br/>

```markdown
![GitHub](/assets/img/github_logo.png "github-logo"){: width="100" height="100" .left }
이미지 `.left` 입니다.
```
![GitHub](/assets/img/github_logo.png "github-logo"){: width="100" height="100" .left }
이미지 `.left` 입니다.
<br/>
<br/>
<br/>
<br/>
<br/>

```markdown
![GitHub](/assets/img/github_logo.png "github-logo"){: width="100" height="100" .right }
이미지 `.right` 입니다.
```

![GitHub](/assets/img/github_logo.png "github-logo"){: width="100" height="100" .right }
이미지 `.right` 입니다.

<br/>
<br/>
<br/>
<br/>

> 주의사항<br/>
> \- 위치 지정을 사용하면 caption을 추가하면 안됩니다.
{: .prompt-warning }

<br/>

---

## 프롬프트 (Prompts)
- `chirpy`에서는 인용문(BlockQuote)을 `info`, `tip`, `warning`, `danger` 4가지 형태로 다르게 표현이 가능합니다.
- 인용문 하단에 `{: .prompt-{type}}` 추가하여 사용

```markdown
> 기본 형태
```
> 기본 형태

<br/>

```markdown
> info prompt
{: .prompt-info }
```

> info prompt
{: .prompt-info }

<br/>

```markdown
> tip prompt
{: .prompt-tip }
```

> tip prompt
{: .prompt-tip }

<br/>

```markdown
> warning prompt
{: .prompt-warning }
```

> warning prompt
{: .prompt-warning }

<br/>

```markdown
> danger prompt
{: .prompt-danger }
```


> danger prompt
{: .prompt-danger }

<br/>

---

## 인라인 코드 (Inline Code)

### 파일경로 강조 (FilePath highlight)
 - \`text\`뒤에 `{: .filepath}`를 추가하여 사용

```markdown
일반 text : /path/tmp/file.md
file path : `/path/tmp/file.md`{: .filepath}
```

일반 text : /path/tmp/file.md <br/>
file path : `/path/tmp/file.md`{: .filepath}

<br/>

---

## 코드블럭 (CodeBlock)
### 줄 번호 (Line Number)
- 기본은 `Line Number`가 표현 되지만 코드블럭 하단에 `{: nolineno }`를 추가하면 `Line Number`를 비활성화 할 수 있습니다.

````markdown
```markdown
- No line setting
- No line setting
- No line setting
```
{: .nolineno }
````

```markdown
- No line setting
- No line setting
- No line setting
```
{: .nolineno }

<br/>

### 파일 이름 지정 (Specifying the Filename)
 - 기본은 코드블럭에 지정한 언어를 표현하지만 `{: file=파일이름 }`를 추가하면 파일이름을 표현 할 수 있습니다.
  

````markdown
```markdown
file path 표시
```
{: file="path/tmp/file" }
````

```markdown
file path 표시
```
{: file="path/tmp/file" }

<br/>

---

## 마무리
`Markdown`으로 기본적으로 표현할 수 있는 것 이외에 `chirpy` Theme에서 사용되는 `Markdown`에 대해서 정리하였습니다. 해당 내용 이외에도 더 많은 내용이 있기 때문에 필요하시면 아래 Link를 참조하시면 됩니다.


<https://chirpy.cotes.page/posts/write-a-new-post/>


<br/>
> 해당 글은 잘못되거나 새로운 내용이 확인되면 언제든 수정될 수 있습니다.
{: .prompt-info }
<br/>


