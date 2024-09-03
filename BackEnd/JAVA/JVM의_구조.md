# JVM의 구조 

## Table of Conetents

1. [JVM의 동작 방식](#jvm의-동작-방식)
2. [JVM의 구조](#jvm의-구조)
3. [Class Loader](#class-loader)
4. [Execution Engine](#execution-engine)
5. [Runtime Data Area](#runtime-data-area)

## JVM의 동작 방식

1. Java 컴파일러(javac)가 Java 소스 코드(*.java)를 바이트 코드(*.class)로 컴파일한다. 
2. Class Loader가 동적 로딩으로 필요한 클래스들을 로딩 및 링크해 Runtime Data Area에 올린다. 
3. Runtime Data Area에 로딩된 바이트 코드는 Execution Engine을 통해 해석된다. 
4. Execution Engine에서 Garbage Collector의 작동, Thread의 동기화가 이루어진다. 

## JVM의 구조

![JVM의 구조](https://upload.wikimedia.org/wikipedia/commons/d/dd/JvmSpec7.png)

## Class Loader

- JVM 내로 클래스 파일(*.class)을 동적으로 로드하고, 링크를 통해 배치하는 작업을 수행하는 모듈
- 로드된 바이트 코드(*.class)들을 엮어 Runtime Data Area에 배치한다.
- 한 번에 모든 클래스를 메모리에 올리지 않는다 : 모든 클래스를 프로그램 실행과 동시에 메모리에 올리지 않는다
- 애플리케이션에 필요한 경우 동적으로 메모리에 적재한다 : 애플리케이션 실행 중 해당 클래스가 실제로 필요해졌을 때 메모리에 로드한다(동적 로딩)
- 메모리의 효율적 관리, 필요한 클래스만 로드함으로써 실행 속도와 메모리 효율성 향상 

클래스 파일의 로딩 순서
- Loading
    - 클래스 파일을 가져와서 JVM의 메모리에 로드
- Linking
    - 로드된 클래스 파일이 사용 가능한 상태가 되도록 연결하는 과정 
    - 1. Verifying(검증) : 클래스 파일이 JVM 규칙에 맞는지 검사한다.
    - 2. Preparation(준비) : 클래스 변수를 메모리에 할당하고 기본값으로 초기화한다. 
    - 3. Resolution(분석) : 심볼릭 레퍼런스(클래스 이름, 필드명 등)를 다이렉트 레퍼런스로 변경해 실제 메모리 주소와 연결한다. 
- Initialization 
    - 클래스의 static 변수들을 초기화, static 블록을 실행한다. 

## Execution Engine

Class Loader를 통해 Runtime Data Area에 배치된 바이트 코드를 명령어 단위로 읽어서 실행한다. 
자바 바이트 코드는 기계가 바로 수행할 수 있는 언어가 아닌, 가상 머신이 이해할 수 있는 중간 레벨로 컴파일된 코드이기 때문에 Execution Engine이 바이트 코드를 실제로 JVM 내부에서 기계가 실행할 수 있는 형태로 변경한다. 

![Execution-Engine](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgvZFHohBTi1Lx0x-MNs4nTJ33MQNs-oIB3k0rKjgtafFgPUwLFF72CIKk8DPs57QFlvivS8W76DX3-edYViv9JvjQwOkXgzRPgj920UI6C3L-2to7LloaLfia9iZOhfwIP7pSbpHvjw80/s640/jvm-architecture+%25281%2529.png)

- Interpreter
    - 바이트 코드 명령어를 하나씩 읽어서 해석하고 바로 실행한다.
    - JVM 안에서 바이트 코드는 기본적으로 인터프리터 방식으로 동작한다. 간단하지만 같은 메소드라도 여러 번 호출되면 매번 해석하고 수행해야 하기 때문에 전체적인 속도가 느리다. 
- JIT Compiler
    - 성능을 높이기 위해 Interpreter의 단점을 보완한다. 
    - 반복되는 코드를 발견해 바이트 코드 전체를 컴파일해 Native Code로 변경한다. 
        - 해당 메소드를 더 이상 인터프리팅 하지 않고, 변환된 코드를 캐시에 저장해 재사용함으로써 속도를 높인다. 
    - JVM은 모든 코드를 JIT compiler 방식으로 실행하지 않고, Interpreter 방식을 사용하다가 일정 기준이 넘어가면 JIT Compiler 방식으로 명령어를 실행한다. 
- Garbage Collector (GC)
    - 메모리 관리 기능을 수행하며, 더 이상 사용하지 않는 객체들을 메모리에서 제거한다. 
    - Heap 메모리 영역에서 더는 사용하지 않는 메모리를 자동으로 회수한다.
        - C언어는 개발자가 직접 메모리를 해제해야 하지만, JAVA의 GC는 자동으로 메모리를 최적화한다. 

## Runtime Data Area

JVM이 실행 중인 자바 애플리케이션의 데이터를 저장하는 메모리 영역

- Method Area 
    - JVM이 시작될 때 생성되는 공간 
    - 클래스, 인터페이스, 메서드, 변수의 바이트 코드를 저장한다. 
    - 프로그램이 시작될 때 로드된다.
- Heap Area 
    - new 연산자로 생성되는 클래스와 인스턴스 변수, 배열 타입 등을 저장하는 공간으로, 동적으로 메모리를 할당한다. 
- Stack Area 
    - FILO(First In Last Out)구조
    - 메서드 호출 시 각 메서드의 상태(지역 변수, 매개 변수, 반환 주소 등의 임시 데이터)를 저장한다. 
- PC Register
    - 현재 실행 중인 JVM 명령어 주소를 저장한다. 
- Native Method Stack Area
    - Native Code(C/C++)로 작성된 메서드의 실행을 지원하기 위한 스택이다. 

참고자료
https://inpa.tistory.com/entry/JAVA-%E2%98%95-JVM-%EB%82%B4%EB%B6%80-%EA%B5%AC%EC%A1%B0-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EC%98%81%EC%97%AD-%EC%8B%AC%ED%99%94%ED%8E%B8
