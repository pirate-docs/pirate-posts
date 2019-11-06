---
title: "JVM"
date: 2019-10-22T15:10:34+09:00
---

## JVM(Java Virtual Machine)이란?

### 역할 
- 어떤 기기, 또는 어떤 운영체제에서도 실행될 수 있게 하는 것 
    - 자바 애플리케이션을 클래스 로더를 통해 읽어서 자바 API와 함께 실행하는 것 
    - Java와 OS 사이의 중개자 역할 수행 
- 프로그램 메모리 관리와 최적화하는 것 
    - 메모리 관리, Garbage Collection을 수행함 
    
<div style="text-align:center" >
    <img src="/static/images/java/jvm.png" />
    <div><b>JVM</b> (출처. <a href="https://www.javaworld.com/article/3272244/what-is-the-jvm-introducing-the-java-virtual-machine.html">What is the JVM - JavaWorld</a>)</div>
</div>

### Java 프로그램 실행과정 

> 1. JVM은 OS로부터 프로그램이 필요로 하는 메모리를 할당받음
>    - JVM이 메모리를 용도에 따라 여러 영역으로 나누어 관리함  
> 2. 자바 컴파일러(javac)가 소스코드(.java)를 읽어서 바이트코드(.class)로 변환 
> 3. Class Loader를 통해 class 파일들을 JVM으로 로딩함 
> 4. 로딩된 class 파일들은 Execution Engine을 통해 해석됨 
> 5. 해석된 바이트코드는 Runtime Data Areas에 배치되어 실행됨 

<div style="text-align:center" >
    <img src="/static/images/java/jvmdiagram.png" />
    <div><b>JVM 아키텍쳐 다이어그램</b> (출처. <a href="https://javatutorial.net/jvm-explained">JVM explained - JavaTutorial</a>)</div>
</div>

### JVM 구성 

- Class Loader 
    - 역할
        - Loading 
        ##### 클래스 이름, 상속관계, 클래스 타입(class, interface, enum), 메서드, 생성자, 멤버변수, 상수 등에 대한 정보를 로딩해서 바이너리 데이터로 변경 
        - Linking
        ##### Verification → Preparation → Resolution 단계를 거쳐 바이트코드 검증 및 메모리 할당 수행 
        - Initialization
        ##### Static block 초기화와 함께 static 데이터들을 할당함 (top → bottom 방식)
    - 구성 
        - Bootstrap Class Loader 
        ##### - JVM이 실행될때 가장 먼저 실행되는 클래스로더 
        ##### - Java 실행에 필요한 기본적인 클래스 로딩 ($JAVA_HOME/jre/lib/rt.jar)
        ##### - Native 언어로 구성되어 있음 
        - Extension Class Loader (Java9 → Platform Class Loader)
        ##### - Bootstrap Class Loader의 자식클래스로 일반적인 java 확장 클래스 로딩 담당
        ##### - Classpath 설정이 없더라도 로딩됨 ($JAVA_HOME/jre/lib/ext 혹은 java.ext.dirs에 등록된 클래스파일) 
        - Application Class Loader (Java9 → System Class Loader)
        ##### - Classpath에 정의되어있거나, -cp, -classpath로 지정된 클래스들이 로딩됨 
        ##### - 애플리케이션의 클래스들을 로드함 
        - User-Defined Class Loader
        ##### - 애플리케이션 코드에 사용자가 직접 정의해서 사용하는 클래스 로더
    - 원칙 
        - 위임 원칙 (Delegation Principle)
        ##### 클래스 로딩이 필요한 시점에 3가지 기본 클래스로더의 윗 방향으로 클래스 로딩을 위임
        ##### ClassLoaderRunner → Internal Class →  
        - 가시범위 원칙 (Visibility Principle)
        ##### 하위 클래스로더는 상위 클래스로더가 로딩한 클래스를 볼 수 있지만, 반대의 경우는 불가능 
        - 유일성 원칙 (Uniqueness Principle)
        ##### 하위 클래스로더는 상위 클래스로더가 로딩한 클래스를 다시 로딩하지 않도록 함 (유일성 보장)
    

- Execution Engine 
    - 로드된 클래스의 바이트코드를 실행하는 Runtime Module
    
    To be continued

- Interpreter

- JIT (Just In Time)

- Garbage Collector