---
title: "네트워크 장비: 허브(Hub), 스위치(Switch)/브리지(Bridge), 라우터(Router) 개념 및 정리"
date: 2022-01-22
last_modified_at: 2022-01-22
header:
  overlay_color: "#20B2AA"
layout: single
classes: wide
categories:
  - network
tags:
  - 네트워크 장비
  - 허브
  - 스위치
  - 라우터

toc: true
toc_sticky: true
toc_label: "목차"
---

_네트워크를 구성 장비에 대해 알아보자_

### 1. 허브

허브는 여러대의 PC가 허브에 연결되어 서도 통신이 가능하도록 돕는다.

허브를 통한 PC간 통신 과정
3대의 PC가 모두 허브에 연결되어있을 경우
1. 1번 PC가 데이터를 허브에 전송(타겟은 3번 PC)
2. 허브는 1번 PC가 연결된 포트 이외의 모든 포트에 데이터를 뿌림
3. 2번 PC는 자신에게 온 데이터가 아니기 때문에 데이터를 버리고, 3번 PC는 자신에게 온 데이터이기 때문에 처리

허브에 연결된 PC는 모두 하나의 콜리전 도메인에 속하므로 한번에 하나의 PC만 통신이 가능하다.

네트워크 조건에 따라 여러 종류의 허브가 있는데 네트워크 환경, 통신 속도, 제공 기능에 따라 여러 종류로 나뉘며 추가로
네트워크 데이터를 분석할 수 있는 인텔리전트 허브와 더미허브지만 인텔리전트 허브와 연결되면 인텔리전트 허브의 기능을 수행하는 세미 인텔리전트 허브도 있습니다.

### 2. 스위치/브리지

#### 2-1. 스위치

스위치는 스위치에 연결된 여러 PC의 동시 통신을 지원한다.

즉 스위치에 5대의 PC가 연결되어 네트워크를 구성한다고 했을 때 1번과 2번 PC간 통신이 진행될 때 3번과 4번 PC간 통신이 진행될 수 있다.

하지만 위 두 통신이 진행 되는동안 5번 PC는 1,2,3,4번 PC와 통신이 진행될 수 없다.

#### 2-2. 브리지

브리지는 스위치의 원조격으로 스위치는 브리지의 기능을 모두 갖고있습니다.

브리지는 말그대로 다리의 역할을 합니다. 여러 PC가 브리지에 연결되면 브리지는 내부적으로 각 PC간 콜리전도메인을 나눕니다.

브리지에 연결된 PC는 자신이 속한 콜리전도메인에 있는 PC와 통신은 다리(브리지)를 건너지 않고 통신이 가능합니다.
하지만 자신이 속한 콜리전도메인 너머의 PC와 통신 시도한다면 반드리 다리(브리지)를 통해 통신을 헤야합니다.

#### 2-3. 스위치/브리지의 기능

브리지/스위치에는 다섯가지 기능이 있습니다.

1. Learning: PC가 통신을 시도할 때 어떤 PC가 연결되어있는지 기억합니다.
2. Flooding: 통신요청이 들어왔을 때 목적지를 모르면 들어온 포트 외에 모든 포트로 통신을 보냅니다.
3. Forwarding: 통신요청이 들어왔을 때 목적지를 안다면 해당 PC가 연결된 포트로 통신을 보냅니다.
4. Filtering: 목적지 이외의 포트로 통신이 나가지 않도록 합니다.
5. Aging: 통신을 한지 오래된 PC에 대한 정보는 사라집니다.

#### 2-4. 스위치/브리지의 차이

1. 스위치는 처리방식이 하드웨어로 이루어지고, 브리지는 소프트웨어적으로 프레임을 처리하기 때문에 스위치가 더 빠릅니다.
2. 브리지는 포트들이 같은 속도를 지원하지만, 스위치는 서로 다른 속도의 포트를 지원합니다.
3. 스위치가 브리지에 비해 제공하는 포트 수가 많습니다.
4. 스위치가 프레임을 처리하는 방식을 더 많이 제공한다.

#### 2-5. Looping과 스패닝 트리

**Looping**: 두 개의 호스트 사이에 두개의 스위치가 있을 때, 하나의 호스트에서 다른 호스트로 가는 경로가 두개 이상있을 때 Looping이 발생합니다.

**스패닝 트리**: Looping의 발생을 방지하기위한 것이 스패닝 트리입니다. 스패닝 트리는 호스트간 두개 이상의 경로가 발생할 경우 하나의 경로를 제외한 모든 경로를 차단해 Looping을 방지합니다. 또한 통신중인 경로에 장애가 발생해 통신이 불가능하게되었을 경우 또 다른 경로를 살려 통신이 가능하도록 합니다.



### 3. 라우터

네트워크 계층(네트워크 3 계층) 장비로, 서로 다른 네트워크를 연결한다.(예시로 LAN과 WAN을 연결해 인터넷을 사용할 수 있도록 한다.)

라우터는 서로 다른 네트워크를 연결하므로, 다른 네트워크와 통신을 하려면 라우터를 반드시 거쳐야한다.

라우터는 연결되어있는 네트워크 별로 IP를 할당 받으며 다른 네트워크와 통신하기 위해 라우터의 IP를 통해 다른 네트워크로 통신이 이뤄진다.

라우터는 목적지를 모르는 프레임이 들어올 경우 모두 차단한다.