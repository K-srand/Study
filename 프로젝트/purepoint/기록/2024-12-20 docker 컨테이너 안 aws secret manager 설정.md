aws secret manager 사용을 위해 awscli를 설치하고 aws configure로 secret key 설정이 필요하다.
하지만 docker 빌드 시 configure 명령어를 사용하여 환경변수를 설정할 수 없다.

따라서 미리 .aws 폴더를 만들고 그 안에 config와 credentials 파일을 만들어 환경변수 값을 저장하고, docker 빌드 시 .aws 폴더를 copy 해주어야한다.


dockerfile

```
# 베이스 이미지 설정 (JDK 17)
FROM openjdk:17-jdk-slim

# 메인 작업 디렉터리 설정
WORKDIR /app

# AWS CLI 설치
RUN apt-get update && \
    apt-get install -y python3-pip && \
    pip3 install awscli && \
    apt-get clean

# 로컬의 .aws 폴더를 컨테이너 내 /root/.aws에 복사
COPY .aws /root/.aws

# 애플리케이션 JAR 파일 복사
COPY ./springboot-purepoint-0.0.1-SNAPSHOT.jar /app/spring-app.jar

# 포트 설정
EXPOSE 8080

# 애플리케이션 실행 명령어
ENTRYPOINT ["java", "-jar", "/app/spring-app.jar"]

```

