## IP Header 
IP Header의 DSCP(Differentiated Service Code Point) 6비트의 DSCP는 각 처리 노드에서 해당 패킷에 대한 처리 방법을 정의하는 PHB를 선택할 때 사용

# 통신을 끊기 위한 RST Packet 전송
TCP Header의 Control Flags(6bit) 필드 값이 RST(Reset)로 설정되어있는 패킷을 생성하여, 서버와 클라이언트 측으로 전송한다.

### Reset Packet 생성
IP Header checksum, TCP Header checksum을 재계산하여 유효한 패킷을 만드는게 중요하며, 각 헤더의 정보를 유효한 값으로 채워야한다.

### RFC 참
RFC 4413 : TCP/IP Field Behavior
https://www.rfc-editor.org/

내용 추가는 다음에~
