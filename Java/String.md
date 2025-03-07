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

CharSequence는 String, Stringbuilder의 상위 타입. 문자열을 처리하는 다양한 객체를 받을 수 있음.
<h3>String 비교 </h3>
`==` : 동일성
`equals()` : 동등성

ex)
String str1 = new String("hello");
String str2 = new String("hello");

str1 == str2의 결과는 false
str1.equals(str2)의 결과는 true

String str1 = "hello";
String str2 = "hello";

str1 == str2와 str1.equals(str2) 둘 다 true
왜 동일성 비교도 true인가? 문자열 풀에 처음 hello 만들어두고, 그 다음에 똑같은 문자열이 들어오면 만들지 않음.

-> 문자열 풀 덕분에 같은 문자를 사용하는 경우 메모리 사용을 줄이고 문자를 만드는 시간도 줄어듦.

풀(Pool) : 자원이 모여있는 곳
프로그래밍에서 풀은 공용 자원을 모아둔 곳을 뜻함.
여러 곳에서 함께 사용할 수 있는객체를 필요할 때마다 생성하고, 제거하는 것은 비효율적
대신에 문자열 풀에 필요한 String 인스턴스를 미리 만들어두고, 여러곳에서 재사용할 수 있다면 성능과 메모리를 더 최적화할 수 있음.
문자열 풀은 힙 영역을 사용함. 문자열 풀에서 문자를 찾을 때는 해시 알고리즘을 사용하므로 매우 빠른 속도로 원하는 String 인스턴스 찾을 수 있음.


문자열 비교는 항상 equals를 사용해서 동등성 비교하는 것을 지향

String은 불변 객체임. 따라서 사이드 이펙트 문제가 발생하지 않음.

불변인 String 클래스의 단점은 문자를 더하거나 변경할 때마다 계속해서 새로운 객체를 생성해야 한다는 점임.
문자를 자주 더하거나 변경해야 하는 상황이라면 더 많은 String 객체를 만들고, GC해야함.

-> CPU, 메모리 자원을 더 많이 사용하게 됨.
문자열의 크기가 클수록, 문자열을 더 자주 변경할수록 시스템의 자원 더 많이 소모

<h3> StringBuilder - 가변 String </h3>
내부의 값을 바로 변경하면 되기 때문에 새로운 객체를 생성할 필요 X
가변의 경우 사이드 이펙트에 주의해서 사용해야함.

![image](https://sj-obsidian-bucket.s3.ap-northeast-2.amazonaws.com/cb6fd45d8894d0fa352d28098beaac7b.png)

![image](https://sj-obsidian-bucket.s3.ap-northeast-2.amazonaws.com/aa8f4ccb8d544e112546d542cf07f429.png)

(java 9 이후)

StrinbBuilder는 보통 문자열을 변경하는 동안만 사용하다가 문자열 변경이 끝나면 안전한(불변) String으로 변환하는 것이 좋음.

<h3> String 변수 최적화 </h3>
String result = str1 + str2

-> String result = new StringBuilder().append(str1).append(str2).toString();
(자바 9부터는 StringConcatFactory를 사용해서 최적화 수행)

자바가 최적화를 처리해주기 때문에 간단한 경우 StringBuilder 사용하지 않아도 됨.
대신 문자열 더하기 연산(+)을 사용하면 충분함.



StringBuilder를 직접 사용하는 것이 더 좋은 경우
- 반복문에서 반복해서 문자를 연결할 때
- 조건문을 통해 동적으로 문자열을 조합할 때
- 복잡한 문자열의 특정 부분을 변경해야 할 때
- 매우 긴 대용량 문자열을 다룰 때

StringBuilder vs StringBuffer
StringBuilder와 똑같은 기능을 수행하는 StringBuffer 클래스도 있음.
StringBuffer는 내부에 동기화가 되어 있어, 멀티 스레드 상황에 안전. 동기화 오버헤드로 인해 성능 느림.
StringBuilder는 멀티 쓰레드 상황에 안전하지 않지만 동기화 오버헤드가 없으므로 속도 빠름.


<h3> 메서드 체이닝 </h3>
메서드 호출의 결과로 자기 자신의 참조값을 반환하면, 반환된 참조값을 사용해서 메서드 호출을 이어갈 수 있음. 
ex) adder.add(1).add(2).add(3).getValue()
.을 찍고 메서드를 계속 연결해서 사용함. 메서드가 체인으로 연결된 것처럼 보임.

코드를 간결하고 읽기 쉽게 한다는 장점이 있음.

![image](https://sj-obsidian-bucket.s3.ap-northeast-2.amazonaws.com/706096512c25e5dd3d307ea15d8ecffc.png)
