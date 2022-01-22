---
title: "GITBLOG: 로컬 개발환경 bundle 에러 해결 for MAC OS"
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
  - 로컬 개발환경 설정

toc: true
toc_sticky: true
toc_label: "목차"
---

_MAC에서 gitblog 개발환경을 구성하며 마주했던 에러를 해결한 과정을 정리해보았다._

#### 개발환경

운영체제: macOS 12.0.1(Monterey)

#### 발생원인

##### - 실행 명령어
```bash
$ bundle
```

##### - 에러메시지
```liquid
Gem::Ext::BuildError: ERROR: Failed to build gem native extension.
...
An error occurred while installing eventmachine (1.2.7), and Bundler cannot continue.
```

#### 해결방법
ruby를 재설치하여 해결했습니다.

```bash
$ brew install ruby

$ brew link --overwrite ruby
```
```
If you need to have ruby first in your PATH, run:
  echo 'export PATH="/usr/local/opt/ruby/bin:$PATH"' >> ~/.zshrc

For compilers to find ruby you may need to set:
  export LDFLAGS="-L/usr/local/opt/ruby/lib"
  export CPPFLAGS="-I/usr/local/opt/ruby/include"
```

위와같이 제공된 ruby 를 PATH에 등록하는 명령어 수행 후

컴파일러가 ruby를 인식할 수 있도록 그 다음 제시된 명령어를 입력하고, .zshrc 파일에 추가로 등록해줍니다.