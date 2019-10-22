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

- 
