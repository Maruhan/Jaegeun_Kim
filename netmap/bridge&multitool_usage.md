# netmap : bridge
netmap에서 기본으로 제공하는 예제인 bridge.c를 통해 IP 할당 없이 bridge 연결 시도.

### 테스트 환경
 - O/S : FreeBSD 10.3 Release
 - 네트워크 드라이브 : e1000, igb
 - 트래픽 : 최대 100Mbps
 
### Interface 설정
 - Promisc 모드 설정
```sh
# ifconfig igb0 promisc up
# ifconfig igb1 promisc up
```
Bridge의 대상이 되는 인터페이스의 경우 promisc 모드를 설정해야 한다. Promisc 란 네트워크 카드의 동작방식 중 하나이며 자신에게 온 패킷이 아니라도 모두 받아 처리하는 모드이다. Bridge의 경우 자신에게 들어오는 패킷 이외에도 모든 패킷을 목적지에 관계없이 동작해야 하기 때문에 반드시 promisc 설정을 한다.

### 빌드 및 실행
 - 빌드의 경우 제공되는 예제와 함께 Makefile이 제공된다.
 - Bridge 연결 인터페이스 : igb0, igb1
```sh
# ./bridge -v -i netmap:igb0 -i netmap:igb1
```
Bridge 실행시 네트워크 드라이버에 따라 다른 결과가 나온다. igb의 경우 바로 bridge 역할을 하지만 e1000의 경우 약 15분 이상 시간이 흐린뒤에 bridge 역할을 한다.
 
# libuinet : multitool
netmap을 이용하여 bridge를 연결하고, 원하는 데이터를 파일로 남기는 것이 가능한 오픈소스

### Interface 설정
 - netmap bridge와 동일하게 Promisc 모드 설정

### 빌드 및 실행
 - 빌드의 경우 제공되는 예제와 함께 Makefile이 제공된다.
 - libuinet의 경우 gmake를 통해 make가 가능
```sh
#./multitool -n em2 -b em3 -n em3 -b em2 -X --listen 0.0.0.0:80 --content-type image/jpeg
```
multitool의 경우 netmap을 통해 bridge를 연결해주며, --content-type에 설정한 대상에 대해 파일로 데이터를 저장한다.

 - content-type
  - application/gzip           // .gz
  - application/json"          // .json
  - application/octet-stream   // .bin
  - application/pdf            // .pdf
  - application/zip            // .zip
  - image/gif                  // .gif
  - image/jpeg                 // .jpg
  - image/png                  // .png
  - text/html                  // .html
  - text/plain                 // .txt
  - text/xml                   // .xml
