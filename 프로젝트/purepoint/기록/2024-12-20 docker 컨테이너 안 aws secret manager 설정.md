aws secret manager 사용을 위해 awscli를 설치하고 aws configure로 secret key 설정이 필요합니다.
하지만 docker 빌드 시 configure 명령어를 사용하여 환경변수를 설정할 수 없습니다.

따라서 미리 .aws 폴더를 만들고 그 안에 config와 credentials 파일을 만들어 환경변수 값을 저장하고, docker 빌드 시 .aws 폴더를 copy 해주었습니다.

<h3>.aws 폴더 안 config, credentials 설정</h3>

.aws/config
```
[default]
region = ap-northeast-2
output = json
```

.aws/credentials
```
[default]
aws_access_key_id = aws access key 값
aws_secret_access_key = aws secret access key 값
```

<h3>dockerfile 설정</h3>
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

<h3>docker-compose.yaml 설정</h3>
```
version: '3.8'

services:
  maria-db-main:
    image: mariadb:10.9
    environment:
      MYSQL_ROOT_PASSWORD: root 계정 패스워드
      MYSQL_DATABASE: 스키마명
      MYSQL_USER: 사용자 계정
      MYSQL_PASSWORD: 사용자 패스워드
    ports:
      - "3306:3306"
    volumes:
      - mariadb-data:/var/lib/mysql

  redis:
    image: redis:7.4.1
    container_name: 컨테이너 이름
    ports:
      - "6379:6379"
    volumes:
      - redis-data:/data
    command: ["redis-server", "--appendonly", "yes"]

  springboot-app:
    build: .
    container_name: springboot-app
    ports:
      - "8080:8080"
    depends_on:
      - maria-db-main
      - redis

volumes:
  mariadb-data:
  redis-data:
```

❌에러 시 참고사항

![image](https://sj-obsidian-bucket.s3.ap-northeast-2.amazonaws.com/f656b7a06a47b8d45d6be008dfacef11.png)
docker-compose로 컨테이너 실행 시 spring datasource url은 localhost를 인식하지 못합니다.
따라서 docker-compose의 DB 컨테이너명와 동일하게 작성해주었습니다.
aws secret manager 환경변수 값을 수정하거나 아래와 같이 임의로 docker-compose springboot 프로젝트 부분에 환경변수를 명시해줌으로써 덮어쓰기하는 방법이 있습니다.
```
ex)
environment:
      - SPRING_DATASOURCE_URL=jdbc:mariadb://{DB컨테이너명}:3306/{스키마명}
      - SPRING_DATASOURCE_USERNAME= DB 계정
      - SPRING_DATASOURCE_PASSWORD= DB 패스워드
      - SPRING_DATASOURCE_DRIVER_CLASS_NAME=org.mariadb.jdbc.Driver
```



