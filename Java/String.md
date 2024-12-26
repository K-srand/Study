int, double, boolean ... 소문자로 시작하는 타입들은 기본형
String ... 대문자로 시작하는 타입들은 객체, 클래스 참조형

String str1 = "hello"
-> String str = new String("hello")로 자바 언어에서는 변경해줌.

<h3> String 클래스 구조 </h3>
![image](https://sj-obsidian-bucket.s3.ap-northeast-2.amazonaws.com/e76c650a816e53a0243eebb346e93950.png)
(java 9 이후)

java 9 이전은 private final char[] value;

