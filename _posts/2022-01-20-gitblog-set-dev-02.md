---
title: "GITBLOG: jekyll 설치 및 실행"
date: 2022-01-20
last_modified_at: 2022-01-20T19:00:00
header:
  overlay_color: "#B8860B"
layout: single
classes: wide
categories:
  - gitblog
tags:
  - gitblog
  - ruby
  - jekyll
  - 로컬 개발환경 설정

toc: true
toc_sticky: true
toc_label: "목차"
---

_로컬에서 테스트 후 배포하기 위해 로컬에 개발환경을 구성해보았습니다._

#### 개발환경

운영체제: macOS 12.0.1(Monterey)

#### jekyll 설치 및 실행
```bash
# jekyll 설치
$ gem install --user-install bundler jekyll
# ruby 버전 확인
$ ruby -v
```

버전 확인시 나오는 첫 두개의 숫자를 X.X에 순서대로 기입하고,
다음 스크립트를 입력해 환경변수를 설정합니다.

```bash
# Z shell 을 사용한다면  
$ echo 'export PATH="$HOME/.gem/ruby/X.X.0/bin:$PATH"' >> ~/.zshrc

# Bash shell 을 사용한다면
$ echo 'export PATH="$HOME/.gem/ruby/X.X.0/bin:$PATH"' >> ~/.bash_profile
```

그 후 블로그 프로젝트 디렉토리로 이동해 블로그를 로컬 PC에서 띄워보겠습니다.

```bash
# build
$ bundle
# 로컬에서 프로젝트 실행
$ jekyll serve
```

만일 bundle스크립스 수행중 `Gem::Ext::BuildError: ERROR: Failed to build gem native extension.`
문제가 발생한다면 다음 포스팅을 참고해주세요.
- [GITBLOG: 로컬 개발환경 bundle 에러 해결 for MAC OS](/gitblog/gitblog-set-dev-01)

위 작업 후에 jekyll을 찾지 못한다면 다음 스크립트를 실행 후 다시 시도해보시길 바랍니다.

```bash
$ sudo gem install -n /usr/local/bin/ jekyll
$ sudo gem install bundler jekyll
```

읽어주셔서 감사합니다.

참고: [https://jekyllrb.com/docs/installation/macos/](https://jekyllrb.com/docs/installation/macos/)