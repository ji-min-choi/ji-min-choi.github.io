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
image = "/img-hugoblog/hugoblog-cover.jpg"
slug = '6'
draft = false
+++

&nbsp;

![github-icon](/img-hugoblog/github-icon.png)

## 1. Hugo를 이용해 깃허브 블로그를 만들게 된 계기

줄곧 '공부한 내용 기록할 블로그 만들어야지' 라고 생각해오긴 했다.
하지만 이렇게 순식간에 만들게 된 가장 큰 이유는 학교에서 듣는 여름방학 몰입교육의 영향이 제일 크다.
몰입교육을 신청한 제일 큰 이유가 나에게 끝없는 자유가 주어진다면 공부는 고사하고 침대 밖으로도 잘 나오지 않을 것이기 때문에 몰입교육이라는 명분이 생긴다면 밖으로 나가 공부할 것이라는 기대였는데 이는 나름 적중했다 볼 수 있다.
몇 달을 생각만 해오던 블로그 구축을 이틀 만에 해냈으니 말이다.

티스토리 블로그를 만들 지 velog 블로그를 만들 지 고민이었는데 깃허브 블로그, 그 중에서도 Hugo를 선택하게 된 계기는 그렇게 대단하지 않다.
티스토리 블로그를 고민하던 이유는 사용자가 블로그를 꾸밀 수 있는 자유도가 높고 왠지 모르겠지만 나에게 티스토리와 velog는 개발자들이 즐겨쓰는 블로그라는 인식이 있었기 때문이다.

그렇게 고민만 하면서 시간을 보내던 중 몰입교육이 시작되었고 깃허브 블로그 만들기라는 과제가 떨어졌다.

깃허브 블로그에는 두 종류가 있다.

> - Ruby 기반의 `Jekyll`
> - Go 기반의 `Hugo`

Jekyll이 만들기 더 쉽고 한국어 자료가 많지만 페이지 수가 몇 없는데도 빌드 시간이 길다는 단점이 있다.
이 점때문에 강사님께서는 Go 기반의 Hugo로 만들어 볼 것을 추천해주셨고 그 결과 이 블로그가 탄생하게 되었다.

&nbsp;

## 2. 블로그를 만들기 위한 환경 세팅

git은 설치되어있다고 가정

### 2.1 Go 설치

[https://go.dev/dl/](https://go.dev/dl/)  
나는 윈도우를 쓰기 때문에 Microsoft Windows로 다운 받아줬다

![Go](/img-hugoblog/installGo.png)

go version로 설치 확인
go version

&nbsp;

### 2.2 Hugo 설치

Hugo extended를 설치하기 위해 `Chocolatey`를 이용한다
파워쉘에 아래 코드를 입력해준다

    Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))

설치가 되지 않는다면 관리자모드로 실행해준다

Chocolatey 설치를 완료했다면 Hugo extended를 설치

    #설치
    choco install hugo-extended

    #Hugo 설치 확인 (버전 및 환경 변수 확인)
    hugo env
    hugo version

&nbsp;

## 3. Hugo site

설치를 완료했다면 이제 Hugo site를 만들자
셸을 열어준다 (나는 Git bash를 이용했다)

새로운 Hugo site를 생성한다

    hugo new site blog

    Congratulations! Your new Hugo site is created in C:\Users\지민\blog.

    Just a few more steps and you're ready to go:

    1. Download a theme into the same-named folder.

    Choose a theme from https://themes.gohugo.io/ or
    create your own with the "hugo new theme <THEMENAME>" command. 2. Perhaps you want to add some content. You can add single files
    with "hugo new <SECTIONNAME>\<FILENAME>.<FORMAT>". 3. Start the built-in live server via "hugo server".

    Visit https://gohugo.io/ for quickstart guide and full documentation.

&nbsp;

## 4. 블로그 테마 선택

블로그에 적용할 테마를 선택해준다
[https://themes.gohugo.io/](https://themes.gohugo.io/)를 참고!

나는 `Stack` 테마를 선택했다

![theme](/img-hugoblog/stack.png)

다운로드를 눌러 제작자의 깃허브 레파지토리로 이동한다
개발자의 레파지토리 주소를 복사

hugo site를 생성한 폴더로 이동한 뒤 테마를 다운받는다

    cd blog
    git submodule add https://github.com/CaiJimmy/hugo-theme-stack.git themes/hugo-theme-stack
    (git submodule add 개발자 레파지토리 주소 themes/테마 이름)

vscode를 열어준다

    code .

`config.toml`을 수정해주는 게 다음 단계이다
받아온 파일을 확인해보니 config.toml이 없고 hugo.toml뿐이었기 때문에 hugo.toml을 config.toml로 rename해주었다

config.toml을 수정하는 건 테마 개발자의 레파지토리에 있는 설명서를 참고하자
테마마다 설정 값이 다를 수 있다

    baseURL = 'https://ji-min-choi.github.io/'
    languageCode = 'en-us'
    title = "Jimin's archive"
    theme = 'hugo-theme-stack'

    [params.defaultImage.opengraph]
    enabled = false

    (baseURL = 'https://깃허브계정.github.io/'
    languageCode = 'en-us'
    title = "블로그 이름"
    theme = '테마 이름'

    [params.defaultImage.opengraph]
    enabled = false)

config.toml에 적은 테마 이름이 맞지 않으면 page 오류가 난다
