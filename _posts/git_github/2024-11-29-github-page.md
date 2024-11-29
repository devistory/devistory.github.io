---
title: GitHub Page 만들기 (theme:chirpy)
date: 2024-11-29 00:00:00 +09:00
description: jekyll의 chirpy theme를 적용한 GitHub Page
categories: [Git，GitHub, GitHub Page]
tags: [GitHub, GitHub Page, GitHub Blog, jekyll, chirpy]     # TAG names should always be lowercase
hidden: false
image:
  path: /assets/img/logo/github_logo.png
  alt: GitHub
---

이 글은 현재 블로그에 적용되어 있는 `jekyll`의 `chirpy` Theme를 기준으로 GitHub Page를 구성하는 방법에 대해서 정리한 글 입니다.

## 사전 준비
GitHub Page를 구성하기 위해서는 다음과 같은 내용들이 사전에 필요합니다.
- GitHub 가입
- Ruby (ver 3.3.6)
- Node.js (ver 20.15.0)

> 참고사항<br/>
> \- `Ruby`, `Node.js`의 version은 제가 설치 했던 환경 정보 입니다.<br/>
> \- `Node.js`는 `chirpy` theme를 초기화할 때 필요
{: .prompt-info }


## 진행 순서
- GitHub Repository 생성
- local 환경에 설치
- 환경 설정
- GitHub Page 배포


## GitHub Repository 생성
`Repository`는 직접 생성 후 `chirpy` Theme를 `Download Zip`하여 직접 연결하는 방법이 있지만 `fork`하는 방식으로 진행 하겠습니다.

- [jekyll-theme-chirpy](https://github.com/cotes2020/jekyll-theme-chirpy/fork) 링크 접속 하여 theme fork
  - Respository name은 `[github 계정].github.io` 형식으로 수정

![Cirpy theme fork](/assets/img/posts/git_github/github-page_01.png)
_Cirpy theme fork_
<br/>

- branch 수정
  - `[github 계정].github.io` repository 선택 - `Settings`
  - Default branch : `master` -> `main`

![Branch setting](/assets/img/posts/git_github/github-page_02.png)
_Branch setting_
<br/>

  - `Settings` - `Branches` - `Add classic branch protection rule` 

![Branch setting](/assets/img/posts/git_github/github-page_03.png)
_Branch setting_
<br/>

  - Branch name pattern : `main` 입력
  - 모든 설정 기본값

![Branch setting](/assets/img/posts/git_github/github-page_04.png)
_Branch setting_
<br/>

## local 환경에 설치

- `[github 계정].github.io` repository 선택 후, url 복사

![repository url clone](/assets/img/posts/git_github/github-page_05.png)
_repository url clone_
<br/>

- local path에서 git clone

```shell
git clone https://github.com/devistory/devistory.github.io.git
```
<br/>

- clone 경로 이동 후, `Cirpy` 초기화

```shell
cd ~/Documents/devistory.github.io
sh ./tools/init.sh
```
<br/>

- `Start Command Prompt with Ruby` 실행
  - 시작(`windows key`) - `Start Command Prompt with Ruby` 

![Start Command Prompt with Ruby](/assets/img/posts/git_github/github-page_06.png)
_Start Command Prompt with Ruby_
<br/>


- `jekyll` 및 패키지 설치

```shell
gem install jekyll
gem install minima
gem install bundler
gem install jekyll-feed
gem install tzinfo-data
```
<br/>

- bundle install

```shell
bundle
```

- jekyll 실행

```shell
bundle exec jekyll serve
```

<br/>

> 참고사항<br/>
> Default port 4000<br/> 
>   \-`127.0.0.1:4000`<br/>
>   \-`localhost:4000`
{: .prompt-info }

<br/>


![jekyll chirpy](/assets/img/posts/git_github/github-page_07.png)
_jekyll chirpy_

<br/>

## 📌 환경 설정
`chirpy` Theme의 설정은 `_config.yml` 파일을 수정 합니다.
<br/>

```yml
lang: ko-KR                             # 언어 설정
timezone: Asia/Seoul                    # 시간 설정
title: devistory                        # blog title
tagline: A text-focused Jekyll theme    # blog sub title
url: "https://devistory.github.io"      # 자신의 github page url 주소
```


> 참고사항<br/>
> \- `_config.yml`을 수정 후 적용하려면 **서비스를 재시작**해야 합니다.<br/>
> \- 위 내용은 `_config.yml`파일의 일부 내용이며 각 항목의 설명은 주석을 참조하면 됩니다.
{: .prompt-info }

<br/>

## GitHub Page 배포

- 확인용 첫 post 작성
  - `_posts` directory에 `2024-11-29-test.md` 파일 생성 후 아래 내용 입력

```markdown
---
title: Test Post
date: 2024-11-29 00:00:00 +09:00
description: 확인용 post 입니다.
categories: [Depth_1, Depth_1_1]
tags: [Test]
hidden: true
---

## 첫 번째 Post 입니다.

```


- 수정 내용 `git push `
  
```shell
git add -A
git commit -m "first commit"
git push
```







## 제목3
- [ ] 빈 박스
- [x] 체크된 박스
- [X] 체크된 박스


## 제목4
```markdown
| header1 | header2 | header3 |
| :------ | :-----: | ------: |
| AAA     |   BBB   |     CCC |
| DDD     |   EEE   |     FFF |
| GGG     |   HHH   |     III |

```

| header1 | header2 | header3 |
| :------ | :-----: | ------: |
| AAA     |   BBB   |     CCC |
| DDD     |   EEE   |     FFF |
| GGG     |   HHH   |     III |


| header1 | header2 | header3 |
| ------- | ------- | ------- |
| AAA     | BBB     | CCC     |
| 111     | 222     | 333     |
| 가가가  | 나나나  | 다다다  |


> info prompt<br/>
> \- 다중??<br/>
> \- 다중??
{: .prompt-info }


> tip prompt
{: .prompt-tip }

> warning
{: .prompt-warning }

> danger
{: .prompt-danger }


{% raw %}
```liquid
{% if product.title contains 'Pack' %}
  This product's title contains the word Pack.
{% endif %}
```
{% endraw %}


뤼키드??