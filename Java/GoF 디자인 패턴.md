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


### 생성 패턴: Builder

목적:
객체의 생성 과정을 단계별로 정의하고, 최종적으로 복합 객체를 만듦.

```
class House {
    private String foundation;
    private String structure;

    static class Builder {
        private String foundation;
        private String structure;

        Builder setFoundation(String foundation) { this.foundation = foundation; return this; }
        Builder setStructure(String structure) { this.structure = structure; return this; }
        House build() { return new House(this); }
    }

    private House(Builder builder) {
        this.foundation = builder.foundation;
        this.structure = builder.structure;
    }
}
```

### 생성 패턴: Prototype

목적:
기존 객체를 복제하여 새로운 객체 생성

```
class Prototype implements Cloneable {
    String field;

    Prototype(String field) { this.field = field; }

    public Prototype clone() {
        try { return (Prototype) super.clone(); }
        catch (CloneNotSupportedException e) { return null; }
    }
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

### 구조 패턴: Bridge

목적:
추상화와 구현을 분리하여 독립적으로 확장 가능하게 함.

```
interface Color { String fill(); }
class Red implements Color { public String fill() { return "Red"; } }

abstract class Shape {
    protected Color color;

    Shape(Color color) { this.color = color; }

    abstract void draw();
}

class Circle extends Shape {
    Circle(Color color) { super(color); }

    void draw() { System.out.println("Drawing Circle with " + color.fill()); }
}
```

### 구조 패턴: Composite

목적:
객체를 트리 구조로 구성하여 단일 객체와 복합 객체를 동일하게 처리

```
interface Component { void render(); }

class Leaf implements Component {
    public void render() { System.out.println("Rendering Leaf"); }
}

class Composite implements Component {
    private List<Component> children = new ArrayList<>();

    void add(Component component) { children.add(component); }
    public void render() {
        for (Component child : children) child.render();
    }
}
```

### 구조 패턴: Decorator

목적:
객체에 동적으로 새로운 기능을 추가함.

```
interface Beverage { String getDescription(); }
class Coffee implements Beverage {
    public String getDescription() { return "Coffee"; }
}

class MilkDecorator implements Beverage {
    private Beverage beverage;

    MilkDecorator(Beverage beverage) { this.beverage = beverage; }

    public String getDescription() { return beverage.getDescription() + ", Milk"; }
}
```

### 구조 패턴: Facade

목적:
복잡한 서브 시스템에 대한 단순화된 인터페이스 제공

```
class SubsystemA { void operationA() { System.out.println("Subsystem A Operation"); } }
class SubsystemB { void operationB() { System.out.println("Subsystem B Operation"); } }

class Facade {
    private SubsystemA a = new SubsystemA();
    private SubsystemB b = new SubsystemB();

    void operation() {
        a.operationA();
        b.operationB();
    }
}
```

### 구조 패턴: Flyweight

목적:
공유 가능한 객체를 재사용하여 메모리를 절약함.

```
class Flyweight {
    private String intrinsicState;

    Flyweight(String state) { this.intrinsicState = state; }

    void operation(String extrinsicState) {
        System.out.println("Intrinsic: " + intrinsicState + ", Extrinsic: " + extrinsicState);
    }
}
```

### 구조 패턴: Proxy

목적:
객체에 접근을 제어하는 대리인을 제공함.

```
interface Service { void request(); }
class RealService implements Service {
    public void request() { System.out.println("Real Service"); }
}

class ProxyService implements Service {
    private RealService realService;

    public void request() {
        if (realService == null) realService = new RealService();
        realService.request();
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