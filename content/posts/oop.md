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

### 다형성 (Polymorphism)

- 하나의 변수명, 함수명 등이 상황에 따라 다른 의미로 해석될 수 있는 것 
    - 서브타입 다형성 (Subtype )

## 참고자료

- [나무위키 - 객체 지향 프로그래밍](https://namu.wiki/w/객체%20지향%20프로그래밍)