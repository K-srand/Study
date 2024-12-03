csrf 활성화로  post 요청이 404 error가 발생하는 경우

-> 임시로 csrf를 비활성화시켜 테스트를 진행해볼 수 있다.
http.csrf(csrf -> csrf.disable());
또는 .csrf(AbstractHttpConfigurer::disable)

그러나 실제 배포 환경에서까지 csrf 비활성화를 할 수는 없기 때문에 다른 방법이 필요하다.

아래는 CSRF 보호 활성화 및 CSRF 토큰을 클라이언트 전달하는 방법에 대한 예시이다.

--------------------------------------------------------------------------

CSRF 보호를 사용하면서 404 오류가 발생하는 이유는 여러 가지가 있을 수 있습니다. 일반적으로 CSRF 보호는 POST, PUT, DELETE와 같은 상태 변경 요청에 대해 CSRF 토큰을 요구합니다. 이를 제대로 설정하지 않으면 요청이 거부되거나 404 오류가 발생할 수 있습니다. 특히, CSRF 토큰을 전달하지 않거나, 잘못된 토큰이 전달되면 Spring Security가 요청을 차단하게 됩니다.

CSRF 보호를 사용하면서 404 오류를 방지하려면 다음과 같은 사항들을 점검하고 설정할 수 있습니다:

![image](https://sj-obsidian-bucket.s3.ap-northeast-2.amazonaws.com/99185ac8df7c82e457117d9edb1c33ed.png)

![image](https://sj-obsidian-bucket.s3.ap-northeast-2.amazonaws.com/99226f3e0786b7ace32af337e2eede47.png)
![image](https://sj-obsidian-bucket.s3.ap-northeast-2.amazonaws.com/8c11ecb4e076325c2e29254b5765c6c8.png)
![image](https://sj-obsidian-bucket.s3.ap-northeast-2.amazonaws.com/fc0a3011a4d60e7f56d1d5e5d6c388fe.png)
