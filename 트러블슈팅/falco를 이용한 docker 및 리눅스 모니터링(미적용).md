
### ⚠️Docker In Docker(DID) 사용 시 고민해야 할 점

위에서 살펴본 것처럼, **==DID==**는 **Container 내부의 Docker CLI**가 **호스트에 설치된 Docker daemon**을 사용합니다. 즉, **==Container 안으로 접근만 할 수 있다면 호스트의 Docker daemon을 제한 없이 사용==**할 수 있는 것이죠.

만약 이를 외부에서 악용한다면 **==심각한 보안 이슈가 발생==**할 수도 있는데요. 그렇기 때문에 DID를 사용할 때엔 **Container 접근과 관련된 보안 설비가 충분히 구축**되어야 안전하겠습니다.

이와 관련해서 **Container 런타임 보안**에 대해 지난 소식지에서 다룬 적이 있으니 참고해보세요 😊
https://maily.so/newslettertodevops/posts/edb58667

[출처] https://maily.so/newslettertodevops/posts/e9o00g04o8w


### falco docker-compose.yml
```
version: '3.8'

services:
  falco:
    image: falcosecurity/falco:latest
    container_name: falco
    privileged: true # Falco가 시스템 호출을 모니터링하려면 필요
    volumes:
      - /var/run/docker.sock:/host/var/run/docker.sock:ro
      - /dev:/host/dev
      - /proc:/host/proc:ro
      - /boot:/host/boot:ro
      - /lib/modules:/host/lib/modules:ro
      - /usr:/host/usr:ro
    environment:
      - FALCO_ENGINE_ARGS="--option"
    network_mode: host # 네트워크 모니터링 활성화
```


