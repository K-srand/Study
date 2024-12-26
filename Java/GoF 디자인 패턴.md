<h3> 1. 생성 패턴: Singleton </h3>
   
목적:
클래스의 인스턴스를 하나로 제한하고, 전역으로 접근할 수 있는 방법 제공

```
public class Singleton {
    // 유일한 인스턴스를 저장할 정적 변수
    private static Singleton instance;

    // private 생성자
    private Singleton() {}

    // 전역 접근 메서드
    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```
```
public class Main {
    public static void main(String[] args) {
        Singleton singleton1 = Singleton.getInstance();
        Singleton singleton2 = Singleton.getInstance();

        System.out.println(singleton1 == singleton2); // true
    }
}
```


<h3> 2. 구조 패턴: Adapter </h3>

목적: 
호환되지 않는 인터페이스를 변환해, 기존 코드와 새 코드 간의 협력을 가능하게 함.

```
// 기존 클래스
class OldSystem {
    public void oldMethod() {
        System.out.println("Old method");
    }
}

// 새 인터페이스
interface NewSystem {
    void newMethod();
}

// 어댑터 클래스
class Adapter implements NewSystem {
    private OldSystem oldSystem;

    public Adapter(OldSystem oldSystem) {
        this.oldSystem = oldSystem;
    }

    @Override
    public void newMethod() {
        oldSystem.oldMethod(); // 기존 메서드 호출
    }
}

public class Main {
    public static void main(String[] args) {
        OldSystem oldSystem = new OldSystem();
        NewSystem adapter = new Adapter(oldSystem);
        adapter.newMethod(); // "Old method" 출력
    }
}
```