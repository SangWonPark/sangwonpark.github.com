---
title: "GITBLOG: 로컬 개발환경 bundle 에러 해결 for MAC OS"
header:
  overlay_color: "#333"
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

### 개발환경

운영체제: macOS 12.0.1(Monterey)

### 발생원인
```bash
$ bundle
```

### 에러메시지
```liquid
Gem::Ext::BuildError: ERROR: Failed to build gem native extension.
...
An error occurred while installing eventmachine (1.2.7), and Bundler cannot continue.
```

### 해결방법
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

컴파일러가 ruby를 인식할 수 있도록 그 다음 제시된 명령어를 입력하고, .zshrc 파일에 추가로 등록해준다.