# Network Layer

네트워크 계층, 3계층이라고 불린다.

데이터를 목적지까지 안전하고 빠르게 전달한다.

# Protocol

3계층에도 프로토콜을 사용한다.

* ARP 프로토콜
* IPv4 프로토콜
* IPv6 프로토콜
* ICMP 프로토콜

여기서 IPv4과 ARP 프로토콜을 살펴보자.

# IPv4

> 192.168.0.189

IPv4는 10진수 단위로 사용된다. 그래서 000.000.0.000 ~ 255.255.255.255 까지 사용할 수 있다.

## 1차 IP

IP를 클래스 단위로 나누어서 사용했다.

> 클래스 단위로 나누면 IP 낭비가 심하다.

## 2차 IP(Classfulless)

클래스 단위로 나누어 사용해서 생기는 낭비를 해결하기 위하여 도입되었다.

> IP를 원하는 곳에서 끊어 네트워크 대역을 구분하기 시작하였다.

이를 지원하기 위해서 **서브넷 마스크**를 도입하기 시작하였다.

### 서브넷 마스크

* 클래스풀한 네트워크 대역을 나눠주는데 사용하는 값
* 어디까지가 네트워크 대역을 구분하는데 사용하고 어디서부터 호스트를 구분하는데 사용하는지 지정
* 2진수로 표기했을 때 1로 시작, 1과 1사이에는 0이 올 수 없다는 규칙을 가지고 있따.

> ex) 255.255.255.192 -> 11111111.11111111.11111111.11000000

위와 같이 나와있을 때, 1이 0으로 바뀌는 부분까지가 네트워크 대역을 나타내는 부분이다.

## 3차 IP(사설 IP와 공인 IP)

현재 사용하고있는 IPv4의 개념이다.

* 공인 IP : 인터넷 세상에서 통신할 때 사용하는 IP 주소이다.
* 사설 IP : 같은 네트워크 대역에서 사용되는 IP 주소이다.

> 다른 네트워크 대역으로 넘어갈 때, 공인 IP 주소로 변경되어 통신이 된다. 하지만 같은 네트워크 대역으로 넘어갈 때는 사설 IP 주소로 이용된다.

이러한 IP 변경작업은 공유기가 해준다!

### 네이버에서 내 IP 주소를 확인해보자.

네이버 입장에서 나의 IP 주소는 공인 IP 주소로 보일 것이다.

공인 IP 주소를 확인해보자.

![image](https://user-images.githubusercontent.com/79268661/188268134-c5ff9eb9-1722-4a56-aa19-92f99fa86e12.png)


위와 같이 나온다.

> 같은 wifi를 사용하는 다른 기기를 사용해도 위와 똑같이 나올 것이다.

그럼 사설 IP 주소룰 확인해보자.

![image](https://user-images.githubusercontent.com/79268661/188268172-8587e3ab-f15c-4599-ad64-d5a14fd2dde9.png)

위와 같이 나온다.

사설 Ip는 해당 wifi에 연결되어있는 모든 기기가 다를 것이다.


> 한마디로 사설 IP가 외부 네트워크 대역으로 넘어갈 때는 공인 IP로 변경되어 통신된다.

이렇게 변경하는 작업을 NAT라고 한다.


> 집에서 인터넷 통신비용으로 주는 것은 공인 IP를 1개 구매했다고 보면 된다.

## 특수한 IP

* 0.0.0.0 : 나머지 IP
* 127.0.0.@ : 자기 자신을 표현하는 IP
* 게이트웨이 주소 : 일반적으로 공유기의 사설 IP를 말한다. 외부으로 나가는 네트워크 주소를 말한다.(공인 IP), 사용할 수 있는 사설 IP에서 가장 큰 IP 또는 가장 작은 IP로 설정된다.

# ARP
> ARP 프로토콜은 같은 네트워크 대역에서 통신을 위해 필요한 MAC 주소를 IP 주소를 통해서 알아오는 프로토콜이다.

같은 네트워크 대역에서 통신을 한다고 하더라도 데이터를 보내기 위해서는 7계층부터 캡슐화를 통해 데이터를 보내기 때문에 _**IP주소와 MAC주소**_가 필요하다.

이 때 IP주소는 알고 MAC 주소는 모르더라도 ARP를 통해서 통신이 가능하다.

## ARP 프로토콜 구조
총 28 bytes 로 구성된다.

![image](https://user-images.githubusercontent.com/79268661/188268195-4d499c9b-aa4a-44f8-b644-d9a9c7d00361.png)


* Hardware type : 하드웨어(MAC) 주소의 유형을 말하며 이더넷 통신시 항상 1로 설정된다.

* Protocol type : 매핑 대상인 프로토콜의 주소의 유형을 나타내며, IPv4의 경우에는 0x0800으로 설정된다.

* Hardware Address Length : 하드웨어 주소(MAC)의 길이를 byte로 나타낸다.

* Protocol Address Length : 프로토콜 주소의 길이를 byte로 나타낸다.

* Opcode: ARP의 동작을 나타낸다.

* Source Hadware Address : 송신자의 MAC 주소를 나타낸다.

* Source Protocol Address : 송신자의 IP 주소를 나타낸다.

* Destination Hardware Address : 수신자의 MAC 주소를 나타낸다.

* Destination Protocol Address : 수신자의 IP 주소를 나타낸다.

# 예시 상황

> 같은 네트워크(LAN) 대역을 사용하는 경우에 A pc가 C pc와 컴퓨터 통신을 하고싶은 상황이다.

1. A pc가 ARP 요청 Protocol을 생성한다. (여기서 목적지 MAC 주소를 00000000~ 으로 채운다.)

2. Ethernet header에는 (FFFFFFFFF로 채운다. -> 브로드캐스트)

3. ARP 요청이 스위치로 이동한다.

4. 스위치는 2계층 프로토콜까지만 확인한다.

5. 스위치는 같은 네트워크 내역 모두에게 ARP 요청(Opcode 1번)을 보낸다.

6. 각 네트워크 장비들은 해당 ARP 요청을 분석(디캡슐화)한다.

7. 2계층, 3계층 까지 확인한다.

8. 3계층의 목적지 IP 주소와 자기 자신의 IP 주소가 맞지 않으면 해당 요청을 버린다.

9. IP 주소가 일치하는 기기(C pc)는 응답 프로토콜(ARP 응답 - Opcode 2번)을 생성하여 만든다.

10. 스위치는 ARP응답을 받고 2계층을 확인한다. 그리고 A pc로 전달한다.

11. A pc는 응답을 받고 3게층까지 분석한 다음 ARP 캐시 테이블에 등록한다.

> 모든 네트워크 작업은 캐시 테이블을 확인하고, 없으면 위의 동작을 수행한다.










