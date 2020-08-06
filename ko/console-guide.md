## Network > Network ACL > 콘솔 사용 가이드

## ACL
ACL 기능에 대한 자세한 사항은 [Network ACL](/Network/Network%20ACL/ko/overview/) 문서를 참고합니다.

#### ACL 생성
ACL을 생성하려면 [ACL 생성] 버튼을 누르고, 다음의 값을 입력합니다.

* 이름: ACL의 이름을 입력합니다.
* 설명: ACL의 설명을 기술합니다.

[확인]을 누르면 ACL이 생성됩니다.

#### ACL 변경
ACL의 속성 중 이름과 설명을 변경할 수 있습니다.

#### ACL 삭제
선택한 ACL을 삭제할 수 있습니다.
ACL에 binding 된 Network이 없을 경우에만 삭제가 가능합니다.

#### ACL Rule 추가
ACL을 선택하면 하단에 ACL Rule 메뉴가 나타납니다.
ACL rule을 추가하면, 이 ACL을 사용하는 모든 network에 추가된 rule이 반영됩니다.

* 프로토콜 : tcp, udp, icmp 등의 프로토콜을 선택합니다.
* src cidr : src ip 혹은 대역을 입력합니다.
* src port : src port 혹은 범위를 입력합니다.
* dst cidr : dst ip 혹은 대역을 입력합니다.
* dst port : dst port 혹은 범위를 입력합니다.
* order : 적용순서를 입력합니다. 해당 룰이 적용되는 우선순위를 의미합니다. order 값이 작은 것부터 먼저 적용됩니다.
* allow/deny : 해당 rule이 허용인지 거부인지를 입력합니다.
* 설명: ACL rule의 설명을 기술합니다.

[확인]을 누르면 ACL rule이 생성됩니다.

> [참고] src와 dst 짝으로 설정하기
>
> 예를 들어 192.168.0.10 주소에서만 192.168.0.13 주소의 tcp 22번으로 접속하는 것을 허용해 주려면 아래와 같이 룰 추가를 해주면 됩니다.
> "protocol"="tcp", "src cidr"="192.168.0.10/32", "dst cidr"="192.168.0.13/32", "dst_port_range_min"=22, "policy"="allow"
> "protocol"="tcp", "src cidr"="192.168.0.13/32", "src_port_range_min"=22, "dst cidr"="192.168.0.10/32", "policy"="allow"
> 해당 주소로 패킷이 들어왔다가 나가야 하는데, 첫 번째 룰만 있을 경우 해당 인스턴스 입장에서 보면 dst는 들어오는 것만 허용해 주는 것이고, 두 번째 룰이 있어야 src로부터 나가는 것이 허용되기 때문입니다.

> [참고] ACL Rule order
>
> acl 생성 시 기본적으로 order number 101번에 모두 허용하는 룰이 들어가고, order number 32765에 모두 거부하는 룰이 들어갑니다.
> 따라서 default 상태는 모든 것이 허용되는 상태가 되고, 이후 사용자가 101번을 지우고 선택적으로 룰을 추가해서 사용할 수 있습니다. (기본 사용 방식은 white list를 관리하는 방식입니다)
> 각 acl의 마지막 rule은 32765의 order number를 가지고 있고, 정책은 모두 거부이며, 삭제가 불가능합니다.
> order number 101번부터 32765번 사이의 값을 사용해서 원하는 rule을 추가할 수 있습니다.
> 1~100번은 내부 시스템용으로 예약되어 있습니다.
> order를 변경하고 싶을 경우, 수정하는 것은 안되고 삭제 후 다시 넣어야 하기 때문에 rule을 설정할 때 10~100 정도의 order number 간격을 두고 설정하는 것이 좋습니다.
> black list를 관리하는 방식으로 바꾸려면, order number 32764에 모든 것을 허용하는 룰을 추가하고, 앞쪽 order number에 black list rule을 관리하면 됩니다.

> [참고] ACL과 ACL Rule 개수
>
> 프로젝트별 ACL을 최대 10개까지 생성할 수 있습니다. 
> 프로젝트별 ACL rule을 최대 100개까지 생성할 수 있습니다.

#### ACL Rule 변경
rule의 속성 중 설명만 변경할 수 있습니다.

#### ACL Rule 삭제
ACL을 선택하면 하단에 ACL Rule 메뉴가 나타납니다.
ACL rule을 삭제하면, 이 ACL을 사용하는 모든 network에서 해당 rule이 삭제됩니다.

#### ACL Binding
ACL을 적용할 network를 선택하고 확인을 누릅니다.
하나의 ACL은 여러 network에 binding 할 수 있습니다.
하나의 network에는 하나의 ACL만 binding 할 수 있습니다.

#### ACL Binding 해제
ACL 적용을 해제할 network을 선택하고 확인을 누릅니다.
