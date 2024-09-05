# JDK vs JRE

## Table of Conetents
1. [JRE (Java Runtime Environment)](#jre-java-runtime-environment)
2. [JDK (Java Development Kit)](#jdk-java-development-kit)
3. [JRE와 JDK](#jre와-jdk)
4. [사용자 디렉터리 구성요소](#사용자-디렉터리-구성요소)
    1. [bin 디렉터리에 들어 있는 주요한 개발 소프트웨어](#bin-디렉터리에-들어-있는-주요한-개발-소프트웨어)

<br>

# JRE (Java Runtime Environment)
- 자바 실행 환경
- 컴퓨터의 운영체제 소프트웨어 상에서 실행
- **컴파일 된 Java 프로그램**을 실행하는 데 필요한 패키지
- 개발(쓰기)은 안 되고 **실행(읽기)만 가능**

자바 가상 머신(Java Virtual Machine), 자바 클래스 라이브러리(Java class library), 자바 명령(Java command) 및 기타 인프라 포함

# JDK (Java Development Kit)
- 자바 개발 키트
- 개발자들이 자바로 개발하는 데 사용
- **프로그램을 생성하고 컴파일**
- Java EE(Java Enterprise Edition), Java SE(Java Special Edition) 또는 Java ME(Java Mobile Edition) 등 Java 버전 및 패키지나 에디션에 따라 JDK를 선택

개발 시 필요한 라이브러리들과 `javac`, `javadoc` 등의 개발 도구들이 포함되어 있음<br>
개발을 하기 위해선 당연히 실행도 시켜야 하기 때문에 **JRE도 함께 포함**<br>

![구조도](https://media.geeksforgeeks.org/wp-content/uploads/20210218150010/JDK.png)

# JRE와 JDK

JRE는 **JDK를 사용하여 작성된 Java 코드**를 JVM에서 이를 실행하는 데 필요한 필수 라이브러리와 결합한 후 결과 프로그램을 실행하는 JVM의 인스턴스를 작성한다.<br>
JVM은 다수의 운영체제에 사용 가능하며, JRE를 사용하여 작성된 프로그램이 이 모두에서 실행된다.<br>
이러한 방식으로, **JRE는 수정 없이도 어떤 운영체제에서든 Java 프로그램을 실행할 수 있도록 한다.**

<br>

![JDK와 JRE 내부 구성](https://www.oracle.com/img/tech/java8-conceptual-design.jpg)

# 사용자 디렉터리 구성요소

JRE는 기본적으로 Java 관련 파일이 있는 디렉터리
- `bin` : 자바 개발, 실행에 필요한 도구와 유틸리티 명령
- `conf` : 여러 종류의 패치 파일
- `include` : 네이티브 코드 프로그래밍에 필요하는 C언어 헤더 파일
- `jmods` : 컴파일된 모듈 파일들
- `legal` : 각 모듈에 대한 저작권과 라이선스 파일
- `lib` : 실행 시간에 필요한 라이브러리 클래스들

## bin 디렉터리에 들어 있는 주요한 개발 소프트웨어
- `javac` : 자바 컴파일러로 자바 소스를 바이트 코드로 변환
- `java` : 자바 프로그램 실행기 → 자바 가상 기계를 작동시켜 자바 프로그램 실행
- `javadoc` : 자바 소스로부터 HTML 형식의 API 도큐먼트 생성
- `jar` : 자바 클래스 파일을 압축한 자바 아카이브 파일(.jar) 생성, 관리
- `jmod` : 자바의 모듈 파일(.jmd)을 만들거나 모듈 파일의 내용 출력
- `jlink` : 응용프로그램에 맞춘 맞춤형 JRE 생성
- `jdb` : 자바 응용프로그램의 실행 중 오류를 찾는 데 사용하는 디버거
- `javap` : 클래스 파일의 바이트 코드를 소스와 함께 보여주는 디어셈블러

<br>

> ✨ 참고<br>
> https://developerntraveler.tistory.com/49
> https://coding-factory.tistory.com/826
> https://www.geeksforgeeks.org/difference-between-jdk-and-jre-in-java/
> https://www.ibm.com/kr-ko/topics/jre
> https://www.oracle.com/java/technologies/platform-glance.html