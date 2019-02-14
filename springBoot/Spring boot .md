# Spring boot 
- 스프링 부트란?
	1. 제품 수준의 어플리케이션을 쉽게 만들수 있다.
	2. 서드파티, 스프링 설정등을 최선의 설정들로 자동 설정 해주어 빠르게 적용할 수 있게 해준다. ex) 톰캣 설정

- 목적
	1. 스프링 개발 시 빠르고 폭넓은 사용성 제공
	2. 일일히 설정 하지 않아도 최선의 설정을 제공 하지만 원하는 설정을 설정할 수 있음
	3. 비즈니스 로직을 구현하는데 필요한 기능 뿐만 아니라 non-functional한 피쳐들(embedded servers, security, metrics, health checks, externalized configuratuin)의 기능 제공
	4. code generation & xml 설정을 더이상 하지 않는다.

# getting-Started

1. 프로젝트 생성
2. pom.xml 파일에 코드 추가 
 
~~~
    <!-- Inherit defaults from Spring Boot 의존성 관리 (부모 프로젝트 설정)-->
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.1.2.RELEASE</version>
    </parent>
    
        <!-- Add typical dependencies for a web application -->
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
    </dependencies>
    
        <!-- Package as an executable jar -->
    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>

~~~


	