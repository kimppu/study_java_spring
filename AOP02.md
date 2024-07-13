# Java spring boot - AOP(2)


## 1. AOP 용어 정리
![alt text](/img/img-aop-03.png)

1) 타겟(Target)
- 핵심 기능을 담고 있는 모듈로 타겟은 부가기능을 부여할 대상(Aspect를 적용하는 곳) <br><br>

2) 어드바이스(Advice)
- 언제 공통 관심 기능을 핵심 로직에 적용할 지를 정의<br><br>

3) 조인포인트(Join Point)
- Advice를 적용 가능한 지점
- 타겟 객체가 구현한 인터페이스의 모든 메서드는 조인 포인트가 됨.<br><br>

4) 포인트 컷(Pointcut)
- JoinPoint의 부분 집합으로서 실제로 Advice가 적용되는 Joinpoint를 표현
- 어드바이스를 적용할 타겟의 메서드를 선별하는 정규표현식<br><br>

5) 애스펙트(Aspect)
- 여러 객체에 공통으로 적용되는 기능
- AOP의 기본 모듈
- Advice + PointCut = Aspect
- 애스펙트는 싱글톤 형태의 객체로 존재 <br><br>

6) 어드바이저(Advisor)
- Advisor = Advice + Pointcut
- 어드바이저는 Spring AOP에서만 사용되는 용어<br><br>

7) 위빙(Weaving)
- 포인트컷에 의해서 결정된 타겟의 조인 포인트에 부가기능(어드바이스)를 삽입하는 과정. 즉, Advice를 핵심 로직 코드에 적용하는 것


---
## 2. AOP 적용 방식
### 1) 컴파일 과정에 삽입하는 방식 : 컴파일 시점 적용
- AspectJ 컴파일러가 일반 .java 파일을 컴파일할 때 부가기능을 넣어서 .class 파일로 컴파일해주는 방식
- Compile-Time 방식은 가장 강력하고 정교한 AOP구현을 제공하지만, 코드 변경과 캄파일이 필요한 점이 단점임.

### 2) 바이트코드를 메모리에 로드하는 과정에 삽입하는 방식 : 클래스 로딩 시점 적용
- JVM내 클래스로더에 .class 파일을 올리는 시점에 바이트 코드를 조작해 부가기능 로직을 추가하는 방식
- 컴파일 이후에도 수정 없이 AOP를 적용할 수 있어 편리하지만 클래스 로더에 종속적일 수 있음.

### 3) proxy pattern 이용 : 런타임 시점 적용
- 컴파일, 클래스 로딩, main() 메서드의 실행 이후에 자바가 제공하는 범위내에 부가 기능을 적용하는 방식으로 이미 런타임 중이라 코드를 조작하기 어려워 스프링, 컨테이너, DI, 빈 등 여러 개념과 기능을 총동원하여 프록시를 통해 부가 기능을 적용하는 방식<p>
- 동적인 AOP구현을 가능하게 하지만 프록시 생성 오버헤드가 발생할 수 있음.

*** 프록시는 메서드 실행 시점에서만 다음 타겟을 호출할 수 있기 때문에, 런타임 시점에 부가기능을 적용하는 방식은 메서드의 실행 지점으로 제한됨.


<br>

### [schema-based approach(xml 기반)](https://docs.spring.io/spring-framework/reference/core/aop/schema.html)

### [@Aspect annotation](https://docs.spring.io/spring-framework/reference/core/aop/ataspectj.html)

