---
title: "OOP (Object-Oriented Programming)"
date: 2019-10-19T11:04:58+09:00
---

## 객체 지향 프로그래밍이란?

- 컴퓨터 프로그래밍의 패러다임 중 하나 
- 프로그램을 명령어의 목록으로 보는 시각에서 벗어나, 여러 개의 독립된 단위(객체)로 파악하고자 하는 것
- 각각의 객체는 메시지를 주고받고, 데이터를 처리할 수 있음 
- 프로그램을 유연하고 변경이 용이하게 만들기 때문에 대규모 소프트웨어 개발에 많이 사용됨 
- 보다 직관적인 코드 분석을 가능하게 하는 장점을 가지고 있음  

## 구성요소

- 클래스 (Class)
    - 사용자 정의 데이터형 (User defined data type)
    - 같은 종류(또는 문제 해결을 위한)의 집단에 속하는 속성(attribute)과 행위(behavior)를 정의한 것 
- 객체 (Object)
    - 클래스의 인스턴스(실제로 메모리에 할당된 것)
    - 자신 고유의 속성(attribute)을 가지며 클래스에서 정의한 행위(behavior)를 수행할 수 있음 
    - 객체의 행위는 클래스에 정의된 행위에 대한 정의를 공유함으로써, 메모리를 경제적으로 사용함 
- 메서드 (Method)
    - 클래스로부터 생성된 객체를 사용하는 방법, 객체에 명령을 내리는 메시지
    - 한 객체의 서브루틴(subroutine) 형태로 객체의 속성을 조작하는데 사용됨 

## 특징 

### 캡슐화 (Encapsulation)

- 필요한 속성(attribute)와 행위(methods)를 하나로 묶음
- 일부를 외부에서 사용하지 못하도록 은닉함 

#### 정보은닉 (Information Hiding)

- 프로그램의 세부 구현을 외부로 드러나지 않도록 특정 모듈 내부로 감추는 것 
- 내부 구현은 감춰서 모듈 내에서의 응집도를 높이고, 외부 노출을 최소화하여 모듈 간의 결합도를 떨어뜨려 유연함과 유지보수성을 높임
- 접근 제한자 종류
    - public : 클래스 외부에서 사용 가능
    - protected : 다른 클래스에는 노출되지 않지만, 상속받은 자식 클래스에는 노출됨
    - private : 클래스 내부에서만 사용되며 외부로 노출되지 않음 
    
{{< expand "Example" >}}
```java
public class Student {
    private String name;

    public void setName(String name) {
        this.name = name;
    }

    public void getName() {
        return name;
    }
}
```

```java
public class School {
    public static void main(String[] ar) {
        Student student = new Student();
        student.setName("홍길동");
        
        System.out.println("Name: " + student.getName());
    }
}
```
    - 변수(name)는 private 접근제어자로 현재 클래스에서만 호출할 수 있도록 함 
    - 필요한 기능만 public 접근제어자로 다른 클래스에서 접근할 수 있도록 함  
{{< /expand >}}

### 상속 (Inheritance)

- 자식 클래스가 부모 클래스의 특성과 기능을 그대로 물려받는 것
- IS-A 관계를 가짐 

### 다형성 (Polymorphism)

- 하나의 변수명, 함수명 등이 상황에 따라 다른 의미로 해석될 수 있는 것 
- 서브타입 다형성 (Subtype Polymorphism / Subtyping)
    #### 기초 클래스 또는 인터페이스를 구현하는 상위 클래스를 생성하고, 해당 클래스를 상속받는 다수의 하위 클래스를 만들어 상위 클래스의 포인터나 참조변수 등이 하위 클래스의 객체를 참조하게 하는 것 
    #### 각 하위 클래스는 상위 클래스의 메서드 위에 자신의 메서드를 덮어쓰는 메서드 오버라이딩을 수행하며, 상위 클래스의 참조변수가 어떤 하위 클래스의 객체를 참조하느냐에 따라 호출되는 메서드가 달라짐 
- 매개변수 다형성 (Parametric Polymorphism)
    #### 타입을 매개변수로 받아서 새로운 타입을 되돌려주는 기능 (컴파일 시 지정한 타입에 따라 해석됨)
    - 템플릿 (Template) 
        ##### - 타입 매개변수를 입력한 타입으로 치환한 코드를 생성하는 방식 (C++)
    - 제네릭 (Generic) 
        ##### 지정한 타입 매개변수에 해당하는 타입만 사용하는 방식 (Java, C#)
- 임시 다형성 (Ad hoc Polymorphism)
    - 함수 오버로딩 (Function overloading) 
        ##### 동일한 이름의 함수를 매개변수에 따라 다른 기능으로 동작하도록 할 수 있음 (C++, C#, Java)
    - 연산자 오버로딩 (Operator overloading) 
        ##### 연산자를 오버로딩하여 기본 연산자가 해당 클래스에 맞는 역할을 수행하게 하는 것 (C++, C#)
- 강제 다형성 (Coercion Polymorphism)
    - 묵시적 형변환 (Implicit type coercion) 
        ##### ex. double a = 30;
    - 명시적 형변환 (Explicit type coercion) 
        ##### ex. double a = (double) 30;
        
## 5대 원칙

### 단일 책임 원칙 (Single Responsibility Principle, SRP)

- 객체는 오직 하나의 책임을 가져야 함 
- 객체는 오직 하나의 변경 이슈만을 가져야 함 

### 개방-폐쇄 원칙 (Open-Close Principle, OCP)

- 객체는 확장에 대해서는 개방적이고 수정에 대해서는 폐쇄적이어야 함
- 객체 기능의 확장을 허용하고 스스로의 변경은 피해야 함 

### 리스코프 치환 원칙 (Liskov Substitution Principle, LSP)

- 자식 클래스는 언제나 자신의 부모 클래스를 대체할 수 있어야 함 

### 인터페이스 분리 원칙 (Interface Segregation Principle, ISP)

- 클라이언트에서 사용하지 않는 메서드는 사용하면 안됨 

### 의존성 역전 원칙 (Dependency Inversion Principle, DIP)
    
- 추상성이 높고 안정적인 클래스는 구체적이고 불안정한 저수준의 클래스에 의존하면 안됨 
- 객체지향의 인터페이스를 통해 해당 원칙을 준수할 수 있음 
    - 추상화한 인터페이스를 구현한 클래스는 클라이언트 변경없이 교체 가능해야 함

## 참고자료

- 나무위키 
    - [객체 지향 프로그래밍](https://namu.wiki/w/%EA%B0%9D%EC%B2%B4%20%EC%A7%80%ED%96%A5%20%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D)
    - [객체 지향 프로그래밍 - 원칙](https://namu.wiki/w/%EA%B0%9D%EC%B2%B4%20%EC%A7%80%ED%96%A5%20%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D/%EC%9B%90%EC%B9%99)