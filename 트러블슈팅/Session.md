![image](https://sj-obsidian-bucket.s3.ap-northeast-2.amazonaws.com/aa75c775e021714a26fcda8e7b7c97e7.png)


![image](https://sj-obsidian-bucket.s3.ap-northeast-2.amazonaws.com/e7f4e3f5caeaad4241afd8f3cf712657.png)


http 사용 시 메서드 간 세션 유지가 안되어 이메일 인증 번호에 null 값이 들어옴.
-> ssl 인증서를 발급받아 https를 사용하여 해결함.


certbot를 설치하여 ssl 인증서 발급

![image](https://sj-obsidian-bucket.s3.ap-northeast-2.amazonaws.com/05c3b70f014933a379e5ee5f141d2e0e.png)



application.properties에 인증서 정보 등록

![image](https://sj-obsidian-bucket.s3.ap-northeast-2.amazonaws.com/77b3131a6b70dc7b6baf205e38c6db99.png)



# Set-Cookie header was blocked because it has ”Secure" attribute ...


![image](https://sj-obsidian-bucket.s3.ap-northeast-2.amazonaws.com/fbe99ae915cc98a50d88ed0bfab3d0ef.png)


docker 볼륨에 ssl 인증키 파일 복사

![image](https://sj-obsidian-bucket.s3.ap-northeast-2.amazonaws.com/72f68bb97b7b8b7c5762554f5c8572ee.png)



nginx.conf에 ssl 사용 설정 등록 

![image](https://sj-obsidian-bucket.s3.ap-northeast-2.amazonaws.com/4d4e2c2dce29fdeef1dd4c61ea2692d0.png)



![image](https://sj-obsidian-bucket.s3.ap-northeast-2.amazonaws.com/1e8a6ceb4496ae814069097209f687a9.png)

