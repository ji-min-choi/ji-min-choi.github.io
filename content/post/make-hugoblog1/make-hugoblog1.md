+++
title = "Hugo를 이용해서 깃허브 블로그 구축하기 - 1"
date = "2023-08-11"
description = "Hugo를 이용해서 Github blog를 만드는 과정"
tags = [
    "github",
    "blog"
]
categories = [
    "Github",
]
image = "/img-hugoblog/hugoblog1/hugoblog-cover.jpg"
slug = '6'
draft = false
+++

&nbsp;

![github-icon](/img-hugoblog/hugoblog1/github-icon.png)

## Hugo를 이용해 깃허브 블로그를 만들게 된 계기

줄곧 '공부한 내용 기록할 블로그 만들어야지' 라고 생각해오긴 했다.  
하지만 이렇게 순식간에 블로그를 만들게 된 시작점엔 여름방학 몰입교육이 위치해있다.  
몰입교육을 신청한 가장 큰 이유가 나에게 끝없는 자유가 주어진다면 공부는 고사하고 침대 밖으로도 잘 나오지 않을 것이기 때문에 몰입교육이라는 명분이 생긴다면 밖으로 나가 공부할 것이라는 기대 때문이었다. 이는 나름 적중했다 볼 수 있다.  
몇 달을 생각만 해오던 블로그 구축을 이틀 만에 해냈으니 말이다.

맨 처음 공부 블로그를 만들자는 생각을 했을 땐 velog를 사용하려 했다.  
개발자들이 많이 사용 중이기도 하고 무난하게 좋아보인다는 게 그 이유였다. (구글링을 하면 velog 글이 많이 보였다)  
그러던 중 [인파님 블로그](https://inpa.tistory.com/)를 접하게 되었다. 해당 블로그를 탐색하며 티스토리의 엄청난 꾸미기 자유도가 확 와닿았다.  
이에 큰 매력을 느꼈고 velog냐 티스토리냐 하는 고민이 시작되었다.

고민만 하며 시간을 보내던 중 몰입교육이 시작되었고 '깃허브 블로그 만들기'라는 과제가 떨어졌다.

깃허브 블로그에는 두 종류가 있다.

> - Ruby 기반의 `Jekyll`
> - Go 기반의 `Hugo`

Jekyll이 만들기 더 쉽고 한국어 자료가 많지만 페이지 수가 몇 없는데도 빌드 시간이 길다는 단점이 있다.
이 점 때문에 강사님께서는 Go 기반의 Hugo로 만들어 볼 것을 추천해주셨고 그 결과 이 블로그가 탄생하게 되었다.

&nbsp;

## 블로그를 만들기 위한 환경 세팅

git은 설치되어있다고 가정

### Go 설치

[https://go.dev/dl/](https://go.dev/dl/)  
나는 윈도우를 쓰기 때문에 Microsoft Windows로 다운받아줬다

![Go](/img-hugoblog/hugoblog1/installGo.png)

```bash
# go 설치 확인
go version
```

&nbsp;

### Hugo 설치

Hugo extended를 설치하기 위해 `Chocolatey`를 이용한다
파워쉘에 아래 코드를 입력해준다

```bash
    Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

설치가 되지 않는다면 관리자모드로 실행해준다

Chocolatey 설치를 완료했다면 `Hugo extended`를 설치

```bash
# 설치
choco install hugo-extended

# Hugo 설치 확인
hugo env
hugo version
```

&nbsp;

## Hugo site

설치를 완료했다면 이제 Hugo site를 만들자
셸을 열어준다 (나는 Git bash를 이용했다)

새로운 Hugo site를 생성한다

```bash
# Hugo site 생성
hugo new site blog

Congratulations! Your new Hugo site is created in C:\Users\지민\blog.

Just a few more steps and you're ready to go:

1. Download a theme into the same-named folder.

Choose a theme from https://themes.gohugo.io/ or
create your own with the "hugo new theme <THEMENAME>" command. 2. Perhaps you want to add some content. You can add single files
with "hugo new <SECTIONNAME>\<FILENAME>.<FORMAT>". 3. Start the built-in live server via "hugo server".

Visit https://gohugo.io/ for quickstart guide and full documentation.
```

&nbsp;

## 블로그 테마 선택

블로그에 적용할 테마를 선택해준다
[https://themes.gohugo.io/](https://themes.gohugo.io/)를 참고

나는 `Stack` 테마를 선택했다

![theme](/img-hugoblog/hugoblog1/stack.png)

선택한 테마의 다운로드를 눌러 제작자의 깃허브 레파지토리로 이동한다
개발자의 레파지토리 주소를 복사

hugo site를 생성한 폴더로 이동한 뒤 테마를 다운받는다

```bash
# hugo site가 있는 폴더로 이동
cd blog

# git
git init

# submodule로 테마 불러오기 (git submodule add 개발자 레파지토리 주소 themes/테마 이름)
git submodule add https://github.com/CaiJimmy/hugo-theme-stack.git themes/hugo-theme-stack
```

vscode를 열어준다

```bash
    code .
```

&nbsp;

## 'config.toml' 수정

`config.toml`을 수정해주는 게 다음 단계이다

받아온 파일을 확인해보니 config.toml이 없고 hugo.toml뿐이었기 때문에 hugo.toml을 config.toml로 rename해주었다

테마 개발자의 레파지토리에 있는 설명서를 참고하여 config.toml을 수정
테마마다 설정 값이 다를 수 있다

```bash
# baseURL = 'https://깃허브계정.github.io/'
# languageCode = 'en-us'
# title = "블로그 이름"
# theme = '테마 이름'

baseURL = 'https://ji-min-choi.github.io/'
languageCode = 'en-us'
title = "Jimin's archive"
theme = 'hugo-theme-stack'

[params.defaultImage.opengraph]
enabled = false
```

![config](/img-hugoblog/hugoblog1/config.png)

config.toml에 적은 테마 이름이 맞지 않으면 오류가 난다

&nbsp;

## hugo server 실행

```bash
# 서버 실행
hugo server
```

    Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
    Press Ctrl+C to stop

서버 실행에 성공하면 해당 문구가 뜬다  
[http://localhost:1313/](http://localhost:1313/)에서 페이지 확인이 가능하다  
서버를 멈추려면 Ctrl+C

![server start image](/img-hugoblog/hugoblog1/server.png)
