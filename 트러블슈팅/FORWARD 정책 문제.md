`FORWARD` 체인의 기본 정책이 `DROP`으로 설정되어 있습니다. 이는 Docker 네트워크와 외부 네트워크 간의 트래픽이 차단될 수 있음을 의미합니다. Docker가 사용하는 네트워크 연결이 제한되지 않도록 규칙을 추가해야 할 수 있습니다.

#### 해결 방법:

다음 명령을 실행하여 `FORWARD` 체인의 정책을 변경하세요:

`sudo iptables -P FORWARD ACCEPT`

Docker 자체 네트워크 정책이 이미 필요한 트래픽을 제어하므로, `FORWARD` 정책을 `ACCEPT`로 변경하는 것이 안전합니다.