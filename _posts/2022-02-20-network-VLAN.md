---
title: "네트워크: VLAN"
date: 2022-02-20T09:03:00+09:00
last_modified_at: 2022-02-20T09:03:00+09:00
header:
  overlay_color: "#5F9EA0"
layout: single
classes: wide
categories:
  - network
tags:
  - 스위치
  - 브리지
  - VLAN

toc: true
toc_sticky: true
toc_label: "목차"
---

_VLAN에 대해 알아보자_

## VLAN이란?

가상의 랜, 'VLAN(Virtual LAN)'이 지원되는 스위치를 사용하면 스위치만으로도 브로드 캐스트도메인을 나눠줄 수 있어. 다양한 부분에서 이점을 볼 수 있습니다.

1. VLAN은 스위치에서 지원하는 기능입니다. 허브나 브릿지에서는 지원하지 않습니다.
2. VLAN은 한 대의 스위치를 여러 개의 네트워크로 나누기 위해 사용됩니다. 그러므로 VLAN으로 나눠지면 오직 라우터를 통해서만 통신이 가능합니다.
3. VLAN을 기준으로 브로드캐스트 도메인이 나눠집니다.
4. 여러대의 스위치를 연결해 병렬로 VLAN을 구성할 수 있습니다. 여러대의 스위치는 **'트렁크 포트(Trunk Port)'**로 연결되어 서로 다은 여러 개의 VLAN을 전송할 수 있습니다.

## Trunking과 VTP(VLAN Trunking Protocol)

트렁킹(Trunking)은 여러 개의 VLAN들을 한번에 실어나르는 것을 말합니다. 모든 VLAN이 하나의 링크로 이동하기 위해 트렁킹이 만들어졌습니다.

두 가지 방식의 트렁킹이 존재합니다. 트렁킹 표준인 'IEEE 802.1Q'방식의 트렁킹과 시스코사에서 만든 ISL트렁킹이 있습니다.

VLAN은 모두 이름을 붙여주는데, 'IEEE 802.1Q' 방식의 트렁킹에서는 딱 하나의 VLAN만 이름을 지어주지 않습니다(=네이티브 VLAN). 
한 VLAN만 이름이 없기 때문에 이름이 없는 패킷은 모두 '이름없는 VLAN'으로 이동하게 됩니다.(=Untagged Traffic)

### VTP(VLAN Trunking Protocol)

VTP는 스위치들 간에 VLAN 정보를 서로 주고 받아 스위치들이 갖고있는 VLAN 정보를 동기화 시켜주기 위한 프로토콜입니다. 
따라서 한 스위치에서 VLAN 정보가 업데이트 되면 VTP가 정보를 업데이트 시켜주기 때문에 다른 스위치에서 같은 작업을 하지 않아도 된다는 이점이 있습니다.

#### VTP간 주고받는 메시지 형식

VTP간 주고받는 메시지는 다음과 같이 'Summary Advertisement', 'Subset Advertisement', 'Advertisement Request' 세가지가 있습니다.

1. Summary Advertisement: 
   - VTP 서버가 연결되어있는 스위치들에게 5분에 한번씩 전달하는 메시지로, 관리하고있는 VTP 도메인 구성에 대한 'Revision Number'를 보냅니다. 
     수신한 스위치들은 'Revision Number'로 자신의 VLAN 정보가 최신인지 아닌지 판단합니다. 또한 VLAN 구성에 변화가 생겼을 때에도 이 메시지가 전달되는데, 이 때는 메시지가 즉시 전달됩니다.
2. Subset Advertisement: 
   - 실제 VLAN 정보가 담겨있는 메시지 입니다. VLAN의 구성이 변경되었을 때나 VTP 클라이언트로부터 'Advertisement Request' 메시지를 받았을 때 전송됩니다.
3. Advertisement Request: 
   - 클라이언트가 VTP 서버에 'Summary Advertisement'나 'Subset Advertisement'를 요청하는 용도로 사용됩니다. 
     클라이언트가 'Summary Advertisement' 메시지로 더 높은 'Revision Number'를 받았거나, VTP 도메인 이름이 바뀌거나, 'Subset Advertisement'를 잃어버렸거나,
     스위치가 새로 리셋되었을 경우 'Advertisement Request'메시지를 VTP 서버에 보냅니다.

#### VTP의 3가지 모드

VTP 서버의 동작을 결정하는 세가지 모드가 존재합니다.

1. VTP 서버 모드: 
   - VTP 서버 모드에서는 VLAN을 생성하고, 삭제하고, VLAN의 이름을 바꿔줄 수 있으며, VTP 도메인 안에 있는 나머지 스위치들에게 VTP 도메인 이름과 VLAN 구성, 
     Configuration Revision Number를 전달해 줄 수 있습니다. 또한 VTP 모든 도메인의 모든 VLAN에 대한 정보를 NVRAM(비 휘발성 램)에서 관리하며, 
     스위치가 꺼졌다 다시 켜지더라도 VLAN 정보를 모두 가지고 있습니다.
2. VTP 클라이언트 모드: 
   - VTP 클라이언트 모드에서는 VLAN 구성을 변경하는 작업을 할 수 없습니다. VTP 서버가 전달해준 VLAN 정보를 받고, 다른 클라이언트로 전달하는것만 가능합니다. 
     또한 VLAN 정보를 NVRAM에 저장하지 않기 때문에 리부팅하면 VLAN정보를 잃게됩니다. 
3. VTP 트랜스페어런트 모드(Transparent Mode): 
   - VTP 트랜스페어런트 모드는 VTP 도메인 영역안에 있지만. VTP 서버의 VLAN 구성을 따르지 않고 VLAN을 독단적으로 구성합니다. 
     독단적인 VLAN구성이기 때문에 VLAN 구성에 변동이있을 때에도 다른 스위치에 알리지 않습니다. 또한 VTP 서버에서 전달받는 VLAN정보는 소모시키지 않고, 연결된 다른 스위치로 전송합니다.
     VLAN 정보를 NVRAM에 저장하기 때문에 리부팅 되어도 VLAN 정보가 남아있습니다. 트랜스페어런트 모드는 로컬 스위치에서만 사용할 VLAN을 가진 스위치에 주로 사용됩니다.

[comment]: <> (#### VTP 동작)

