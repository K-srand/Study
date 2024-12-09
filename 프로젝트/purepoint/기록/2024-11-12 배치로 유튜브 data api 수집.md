카테고리별 데이터 받아오기
-> query에 카테고리 값 넣기
DB 담을 때는 ID 값으로 넣기

video 데이터 넘겨주는 로직 구현 O

쇼츠나 너무 짧은 영상 제외
videoDuration
- `**any**` – 동영상 길이를 기준으로 동영상 검색결과를 필터링하지 않습니다. 기본값입니다.
- `**long**` – 20분보다 긴 동영상만 포함합니다.
- `**medium**` – 4분 이상 20분 이하인 동영상만 포함합니다.
- `**short**` – 4분 미만인 동영상만 포함합니다.

강의 목록 페이지에 영상 출력할 때 어떤순으로 영상을 보여줄 것인지


cron 설치 방법(미설치 시)
```
sudo apt-get update
sudo apt-get install cron
```

cron 실행 확인
```
service cron status
service cron start
service cron stop
service cron restart
```

cron 설정 방법
```
crontab -e : 크론탭 등록/수정
crontab -l : 크론탭 리스트 보기
crontab -r : 크론탭 작업 모두 삭제
crontab /path/to/file : 특정 파일로 크론탭 설정
crontab -i -r /path/to/file : 특정 파일에서 크론탭 작업 삭제
```
```
*  *  *  *  * /경로/파일.sh
분(0-59), 시(0-23), 일(1-31), 월(1-12), 요일(0-6, 일요일부터 시작)
```

### ".sh 자체는 실행이 되는데 crontab에 저장한 내용은 실행이 안되는 경우"
명령어로 직접 sh 파일을 실행하면 되지만 crontab에 작성한 내용은 실행이 안되는 경우, 거진 **"실행 권한"** 문제다
Crontab에서 스크립트를 실행하려면 그 스크립트 파일이 실행 가능한 상태여야 한다.
ex) 
```
chmod +x /경로/파일.sh
```



