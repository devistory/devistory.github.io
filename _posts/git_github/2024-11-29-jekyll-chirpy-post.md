---
title: GitHub Page 글쓰기 (theme:chirpy)
date: 2024-11-29 00:00:00 +09:00
description: jekyll의 chirpy theme를 적용한 GitHub Page, post 작성 방법
categories: [Git，GitHub, GitHub Page]
tags: [GitHub, GitHub Page, GitHub Blog, jekyll, chirpy]
hidden: false
image:
  path: /assets/img/logo/github_logo.png
  alt: GitHub
---

이 글은 `jekyll`의 `chirpy` Theme에서 post를 작성하는 방법에 대해서 정리한 글 입니다.

<br/>

---

## 사전 준비
GitHub Page에 글을 쓰기 위해서는 다음과 같은 내용들이 사전에 필요합니다.
- chirpy theme가 적용된 GitHub Page
- VS Code
- Markdown


> **참고사항**<br/>
> `VS Code`는 필수는 아니지만 `Markdown`을 지원하는 Editor가 있으면 좀 더 편리하게 글을 작성할 수 있습니다.
{: .prompt-info }

<br/>

---


## Directory 구조
- `chirpy` Theme에서 새로운 글을 작성하기 위해서는 `_posts`와 `assets` Directory가 필요합니다.
  - `_posts` : `DockHub Page` 글을 관리하는 Directory
  - `_assets` : `DockHub Page` image를 관리하는 Directory

<br/>

---

## 글 작성 방법
### `.md` 파일 이름 규칙
- `.md` 파일은 `[year]-[month]-[day]-[파일이름].md` 형식으로 작성해야 합니다.

```
2024-11-29-new-post.md
2024-11-29-testpost.md
```

### `.md` 파일 작성 규칙
- `.md` 파일은 `_posts` Directory 내에 작성해야 합니다.
- `chirpy` Theme에서 글을 쓰기 위해서는 `.md`파일을 아래와 같이 정의된 양식에 맞혀 글을 작성해야 합니다.

```markdown
---
title: GitHub Page 만들기 (theme:chirpy)
date: 2024-11-29 00:00:00 +09:00
description: jekyll의 chirpy theme를 적용한 GitHub Page
categories: [Git，GitHub, GitHub Page]
tags: [GitHub, GitHub Page, GitHub Blog, jekyll, chirpy]
hidden: false
image:
  path: /assets/img/logo/github_logo.png
  alt: GitHub
---

...본문 내용...
```

![Post Example results](/assets/img/posts/git_github/github-post_01.png){: .shadow }
_Home 화면에 표현되는 post<br/>(title, description, date, categories, image)_

<br/>

![Post Example results](/assets/img/posts/git_github/github-post_02.png){: .shadow }
_post 상단<br/>(title, description, date, image, name)_

<br/>

![Post Example results](/assets/img/posts/git_github/github-post_03.png){: .shadow }
_post 하단<br/>(categories, tags)_


<br/>


- 본문 내용을 작성할 때는 `Markdown`을 사용하여 작성해야 합니다.
  - `Markdown` 기본 문법은 [여기](https://devistory.github.io/posts/markdown-basic/ "markdown-basic")를 참고하시기 바랍니다.
  - `chirpy` Theme에서 사용할 수 있는 문법은 [여기](https://devistory.github.io/posts/markdown_chirpy/ "markdown-chirpy")를 참고하시기 바랍니다.

```markdown

---
title: Test Post
date: 2024-11-30 00:00:00 +09:00
description: Test Post입니다. 
categories: [github, github_page]
tags: [GitHub, GitHub Page, GitHub Blog, jekyll, chirpy]
hidden: false
---


> 첫 번째 Post 입니다. <br/>

post 내용은 `markdown`으로 작성해야 합니다.

```
{: file="_posts/test/2024-11-30-test_post.md" }

![Post Example results](/assets/img/posts/git_github/github-post_04.png){: .shadow }
_Home에 표현되는 post_

<br/>

![Post Example results](/assets/img/posts/git_github/github-post_05.png){: .shadow }
_Category 구조_

<br/>

![Post Example results](/assets/img/posts/git_github/github-post_06.png){: .shadow }
_Post 내용_


<br/>

---

## 이미지 추가
 - 이미지는 `/assets/img` Directory에 저장하여 사용

> **주의**<br/>
>  \- 위 경로가 아니면 이미지가 제대로 호출되지 않습니다.
{: .prompt-warning }

```markdown

---
title: Test Post
date: 2024-11-30 00:00:00 +09:00
description: Test Post입니다. 
categories: [github, github_page]
tags: [GitHub, GitHub Page, GitHub Blog, jekyll, chirpy]
hidden: false
---


> 첫 번째 Post 입니다. <br/>

post 내용은 `markdown`으로 작성해야 합니다.

 - 이미지 추가
  
![GitHubLogo](/assets/img/logo/github_logo.png)
_GitHub Logo_

```
{: file="_posts/test/2024-11-30-test_post.md" }

![Post image example results](/assets/img/posts/git_github/github-post_07.png){: .shadow }
_Post image example results_


<br/>

---

## 마무리
`chirpy` Theme에서 post를 작성하기 위한 방법에 대해서 정리하였습니다.<br/>
post를 배포하는 방법은 [여기](https://devistory.github.io/posts/github-page/#github-page-%EB%B0%B0%ED%8F%AC "github-page")를 참조하시기 바랍니다.

<br/>

📑 **참고 자료**
- [JSDevBlog](https://jason9288.github.io/posts/github_blog_1/)
- [하얀눈길 블로그](https://www.irgroup.org/posts/jekyll-chirpy/)
- [Dodev 블로그](https://wlqmffl0102.github.io/posts/Making-Git-blogs-for-beginners-1/)
- [NUGALOG 블로그](https://nugabox.github.io/posts/jekyll-Chirpy%EB%A1%9C-GitHub-Pages-%EB%A7%8C%EB%93%A4%EA%B8%B0/#branch-%EB%B3%80%EA%B2%BD)
- [JJIKIN 블로그](https://jjikin.com/posts/Jekyll-Chirpy-%ED%85%8C%EB%A7%88%EB%A5%BC-%ED%99%9C%EC%9A%A9%ED%95%9C-Github-%EB%B8%94%EB%A1%9C%EA%B7%B8-%EB%A7%8C%EB%93%A4%EA%B8%B0(2023-6%EC%9B%94-%EA%B8%B0%EC%A4%80)/)
- [Simple Record 블로그](https://friendlyvillain.github.io/posts/chirpy-setup/)

<br/>
> 해당 글은 잘못되거나 새로운 내용이 확인되면 언제든 수정될 수 있습니다.
{: .prompt-info }
<br/>