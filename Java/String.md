int, double, boolean ... 소문자로 시작하는 타입들은 기본형
String ... 대문자로 시작하는 타입들은 객체, 클래스 참조형

String str1 = "hello"
-> String str = new String("hello")로 자바 언어에서는 변경해줌.

<h3> String 클래스 구조 </h3>
![image](https://sj-obsidian-bucket.s3.ap-northeast-2.amazonaws.com/e76c650a816e53a0243eebb346e93950.png)
(java 9 이후)

java 9 이전은 private final char[] value;

자바에서 문자 하나를 표현하는 `char`는 2byte를 차지함.
영어, 숫자는 보통 1byte로 표현이 가능함.
그래서 단순 영어, 숫자로만 표현된 경우 1byte를 사용하고(정확히는 Latin-1 인코딩의 경우 1byte 사용), 그렇지 않은 나머지의 경우 2byte인 UTF-16 인코딩 사용함.
-> 메모리를 더 효율적으로 사용할 수 있게 됨.

**주요 메서드**
length()
charAt()
substring()
indexOf()
toLowerCase(), toUpperCase()
trim()
concat()

