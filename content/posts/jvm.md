---
title: "JVM"
date: 2019-10-22T15:10:34+09:00
---

# JVM(Java Virtual Machine)이란?

## 역할 
어떤 기기, 또는 어떤 운영체제에서도 실행될 수 있게 하는 것  
프로그램 메모리 관리와 최적화하는 것 

- 자바 애플리케이션을 클래스 로더를 통해 읽어서 자바 API와 함께 실행 
- Java와 OS 사이의 중개자 역할 수행 
- 메모리 관리, Garbage Collection을 수행
    
<div style="text-align:center" >
    <img src="/static/images/java/jvm.png" />
    <div><b>JVM</b> (출처. <a href="https://www.javaworld.com/article/3272244/what-is-the-jvm-introducing-the-java-virtual-machine.html">What is the JVM - JavaWorld</a>)</div>
</div>

## Java 프로그램 실행과정 

> 1. JVM은 OS로부터 프로그램이 필요로 하는 메모리를 할당받음  
>    (JVM이 메모리를 용도에 따라 여러 영역으로 나누어 관리함)  
> 2. 자바 컴파일러(javac)가 소스코드(.java)를 읽어서 바이트코드(.class)로 변환 
> 3. Class Loader를 통해 class 파일들을 JVM으로 로딩함 
> 4. 로딩된 class 파일들은 Execution Engine을 통해 해석됨 
> 5. 해석된 바이트코드는 Runtime Data Areas에 배치되어 실행됨 

<div style="text-align:center" >
    <img src="/static/images/java/jvmdiagram.png" />
    <div><b>JVM 아키텍쳐 다이어그램</b> (출처. <a href="https://javatutorial.net/jvm-explained">JVM explained - JavaTutorial</a>)</div>
</div>

## JVM 구성 

클래스로더, 실행엔진, 데이터영역으로 구분됨 

### Class Loader 
#### 역할
- Loading  
클래스 이름, 상속관계, 클래스 타입(class, interface, enum), 메서드, 생성자, 멤버변수, 상수 등에 대한 정보를 로딩해서 바이너리 데이터로 변경
 
- Linking  
바이트코드 검증 및 메모리 할당 수행  
Verification → Preparation → Resolution 단계를 거침
 
- Initialization  
Static block 초기화와 함께 static 데이터들을 할당함 (top → bottom 방식)

#### 구성 
- Bootstrap Class Loader 
    - JVM이 실행될때 가장 먼저 실행되는 클래스로더 
    - Native 언어로 구성되어 있음 
    - Java 실행에 필요한 기본적인 클래스 로딩  
    - $JAVA_HOME/jre/lib/rt.jar
    
- Extension Class Loader (Java9 → Platform Class Loader)
    - Bootstrap Class Loader의 자식클래스
    - 일반적인 java 확장 클래스 로딩 담당
    - Classpath 설정이 없더라도 로딩됨  
    - $JAVA_HOME/jre/lib/ext 혹은 java.ext.dirs에 등록된 클래스파일 
    
- Application Class Loader (Java9 → System Class Loader)
    - Classpath에 정의되어있거나, -cp, -classpath로 지정된 클래스들이 로딩됨 
    - 애플리케이션의 클래스들을 로드함
    
- User-Defined Class Loader
    - 애플리케이션 코드에 사용자가 직접 정의해서 사용하는 클래스 로더

#### 원칙 
- 위임 원칙 (Delegation Principle)
    - 3가지 기본 클래스로더의 윗 방향으로 클래스 로딩을 위임
    - ClassLoaderRunner → Application ClassLoader → Extension ClassLoader → Bootstrap ClassLoader
    
- 가시범위 원칙 (Visibility Principle)
    - 하위 클래스로더는 상위 클래스로더가 로딩한 클래스를 볼 수 있음
    - 반대의 경우는 불가능 
    
- 유일성 원칙 (Uniqueness Principle)
    - 하위 클래스로더는 상위 클래스로더가 로딩한 클래스를 다시 로딩하지 않도록 함 
    - 유일성 보장

### Execution Engine 
- 로드된 클래스의 바이트코드를 실행하는 런타임 모듈
- 클래스 로드 작업이 끝난 클래스 파일은 Runtime Data Area의 Method Area 배치됨 
- Method Area의 바이트코드를 Execution Engine으로 제공하여 실행할 수 있도록 제공  
  (참고. Instruction : Execution Engine 수행하는 가장 최소 단위의 명령어) 
- 처리방식 
    - Interpreter 방식 (JVM 최초 버전)  
    바이트코드를 한 라인씩 이릭고 해석하여 실행 
    - JIT (Just In Time) Compiler 방식  
    바이트코드를 JIT Compiler 통해서 어셈블러 같은 native code로 변경되어 실행  
    실행속도는 빠르지만, 어셈블러 코드 변경 비용발생 (반복 수행이 많을 경우 유리함)  
    - Interpreter + JIT Compiler 방식으로 실행됨 

### Runtime Data Area 
프로그램을 수행하기 위해 OS에서 할당받은 메모리 공간 

#### PC Register
- 스레드 시작시 생성됨 (스레드마다 하나씩 존재)
- 스레드가 어떤 부분을 어떤 명령으로 실행해야 할지에 대한 기록을 하는 부분  
- 현재 수행 중인 JVM 명령의 주소를 가짐 

#### JVM Stack
- 프로그램 실행과정에서 임시로 할당되었다가 메서드가 끝나면 바로 소멸되는 데이터 저장 
- 변수나 임시 데이터, 스레드, 메서드의 정보를 저장함 
- 메서드 호출시마다 각각의 스택 프레임이 생성됨
- 호출된 메서드의 매개변수, 지역변수, 리턴 값, 연산시 일어나는 값을 임시로 저장 

#### Native method stack
- 실제 실행할 수 있는 기계어로 작성된 프로그램을 실행시키는 영역 
- Java가 아닌 다른 언어로 작성된 코드를 위한 공간
- Java Native Interface를 통해 바이트코드로 변환하여 저장함 

#### Method Area (Class area, Static area)
- 클래스 정보를 처음 메모리 공간에 올릴때 초기화되는 대상을 저장하기 위한 메모리 공간 
- 프로그램의 흐름을 구성하는 바이트코드가 저장됨 
- main 메서드부터 컴파일된 바이트코드 대부분이 저장된다고 볼 수 있음 
- Runtime Constant Pool이라는 별도의 관리 영역도 함께 존재함 
- 저장되는 정보의 종류
    - Field Information  
    멤버변수의 이름, 데이터 타입, 접근제어자에 대한 정보
    - Method Information  
    메서드 이름, 리턴타입, 매개변수, 접근제어자에 대한 정보 
    - Type Information  
    Type 속성(class, interface 여부), 이름, super class 전체 이름 저장  

#### Heap 
- 객체를 저장하는 가상 메모리 공간 
- 영역 구분
    - Permanet Generation  
    생성된 객체 정보의 주소값이 저장된 공간  
    Class, method 등에 대한 메타정보가 저장되는 영역  
    Reflection으로 동적으로 클래스가 로딩되는 경우에 사용됨 
    - New/Young area  
    Eden : 객체들이 최초로 생성되는 공간  
    Survivor 0/1 : Eden에서 참조되는 객체들이 저장되는 공간 
    - Old area  
    New area에서 일정시간 참조되는, 살아남은 객체들이 저장되는 공간    
    1) Eden 영역에 객체가 가득차게 되면 minor GC 발생  
    2) Eden 영역에 있는 값들은 survivor 1 영역에 복사되고, 나머지 영역의 객체는 삭제