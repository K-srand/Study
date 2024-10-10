순수 JDBC는 Connection으로 DB 연결 후 메서드 안에 직접 SQL문을 작성하고 데이터 조회, 수정 등의 과정을 while문이나 if문으로 한 줄 한 줄 받아와야 함. 그리고 마지막에 DB close를 하는 형태.
DataSource 직접 주입
-> 비효율적

스프링부트는 구현체만 바꾸면 됨.
애플리케이션 조립 코드(config파일)만 수정해주면 사용 가능

기존 코드 손대지 않고, 설정만으로 구현 클래스 변경 가능(개방-폐쇄 원칙)
-> 다형성


@Autowired로 테스트 케이스 만들기

스프링 컨테이너를 사용하지 않고 단위 테스트를 진행하는것이 좋다.

JDBCTemplate과 Mybatis와 같은 라이브러리는 중복 코드를 제거해준다. SQL문은 직접 작성해야한다.


SimpleJdbcInsert -> SQL문 작성X, 간단하게 데이터 입력 가능

spring.jpa.hibernate.ddl-auto=none : JPA는 객체를 보고 테이블을 자동으로 만듦. 자동으로 만드는 것을 해제함.
