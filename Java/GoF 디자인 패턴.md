### 생성 패턴: Singleton
   
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

public class Main {
    public static void main(String[] args) {
        Singleton singleton1 = Singleton.getInstance();
        Singleton singleton2 = Singleton.getInstance();

        System.out.println(singleton1 == singleton2); // true
    }
}
```


### 생성 패턴: Factory Method

목적:
객체 생성을 서브클래스에 위임.

```
abstract class Product {
    abstract void use();
}

class ConcreteProductA extends Product {
    void use() { System.out.println("Product A"); }
}

class ConcreteProductB extends Product {
    void use() { System.out.println("Product B"); }
}

abstract class Creator {
    abstract Product factoryMethod();
}

class CreatorA extends Creator {
    Product factoryMethod() { return new ConcreteProductA(); }
}

class CreatorB extends Creator {
    Product factoryMethod() { return new ConcreteProductB(); }
}

```

### 생성 패턴: Abstract Factory

목적:
관련 객체 군을 생성하기 위한 인터페이스 제공

```
interface Chair { void sitOn(); }
interface Table { void use(); }

class ModernChair implements Chair {
    public void sitOn() { System.out.println("Sitting on Modern Chair"); }
}

class VictorianChair implements Chair {
    public void sitOn() { System.out.println("Sitting on Victorian Chair"); }
}

interface FurnitureFactory {
    Chair createChair();
    Table createTable();
}

class ModernFurnitureFactory implements FurnitureFactory {
    public Chair createChair() { return new ModernChair(); }
    public Table createTable() { return null; } // Table 생략
}
```


### 구조 패턴: Adapter

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

### 행위 패턴: Observer

목적:
객체 간 일대다 관계를 정의하여 한 객체의 상태 변경 시 관련된 다른 객체들이 자동으로 업데이트되도록 함.

```
import java.util.ArrayList;
import java.util.List;

// 옵저버 인터페이스
interface Observer {
    void update(String message);
}

// 구독 가능한 주체
class Subject {
    private List<Observer> observers = new ArrayList<>();

    public void addObserver(Observer observer) {
        observers.add(observer);
    }

    public void removeObserver(Observer observer) {
        observers.remove(observer);
    }

    public void notifyObservers(String message) {
        for (Observer observer : observers) {
            observer.update(message);
        }
    }
}

// 구독자 클래스
class Subscriber implements Observer {
    private String name;

    public Subscriber(String name) {
        this.name = name;
    }

    @Override
    public void update(String message) {
        System.out.println(name + " received: " + message);
    }
}

public class Main {
    public static void main(String[] args) {
        Subject subject = new Subject();

        Observer subscriber1 = new Subscriber("Subscriber 1");
        Observer subscriber2 = new Subscriber("Subscriber 2");

        subject.addObserver(subscriber1);
        subject.addObserver(subscriber2);

        subject.notifyObservers("New event occurred!");
    }
}
```