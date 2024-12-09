https://365kim.tistory.com/93


https://blog.happykoo.net/@wando/posts/326

유튜브 data api를 사용하여 데이터 첫 호출 시 대략 500개의 데이터만 가져올 수 있었음.
totalresults는 100000 값이 들어가 있는데 50개씩 약 10번의 호출 후 nextPageToken을 제공하지 않아 배치 프로세스가 중단되었음.
구글의 제한으로 totalresults를 모두 가져오기는 어려워 보임.
두 번째 요청 시 몇십개의 데이터가 추가됨.
