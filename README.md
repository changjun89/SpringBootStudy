의존성 관리 이해

스프링 부트는 parent의 상속 구조를 사용해서 의존성 관리를 쉽게해준다.

상위 parnet

<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.1.2.RELEASE</version>
</parent>


상위 parant의 parant spring-boot-dependencies

<groupId>org.springframework.boot</groupId>
<artifactId>spring-boot-dependencies</artifactId>
<version>2.1.2.RELEASE</version>


spring-boot-dependencies 에서 하위 처럼 dependencyManegement에서 dependency들과 버전들을 관리해 주기 때문에 dependencyManagement 에서 관리해주는 dependency들을 추가할때는 버전을 명시하지 않아도 자동으로 설정되어 있는 버전을 가지고 오게 된다. 



 이로인한 이점으로

1. 관리해야 하는 의존성들이 줄어든다.

2. springversion 혹은 third-part의 버전을 올려야 할 때 등의 호환성을 고려하지 않고 사용할 수 있다. 



<properties>
    <activemq.version>5.15.8</activemq.version>
    <antlr2.version>2.7.7</antlr2.version>
    <appengine-sdk.version>1.9.71</appengine-sdk.version>
    <artemis.version>2.6.3</artemis.version>


<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot</artifactId>
            <version>2.1.2.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-test</artifactId>
            <version>2.1.2.RELEASE</version>
        </dependency>




springboot pom에서 자동으로 설정해주는 version이 아닌 다른 버전을 사용을 원할시에는 <version></version> 에 버전을 입력하게 되면 입력한 버전이 오버라이딩 하기 때문에 해당 버전을 사용할 수 있다.



springBoot의 pom을 사용하지 않고 싶을 때

<dependencyManagement>
		<dependencies>
		<dependency>
			<!-- Import dependency management from Spring Boot -->
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-dependencies</artifactId>
			<version>2.1.2.RELEASE</version>
			<type>pom</type>
			<scope>import</scope>
		</dependency>
	</dependencies>
</dependencyManagement>
단 단점은 dependeny 이외의 설정들 properties, plugin 설정 들이 먹히지 않는다.

parant pom을 추천한다.

*참조 레퍼런스

https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#using-boot-dependency-management


의존성관리 응용

1. 버전 관리 해주는 의존성 추가

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
버전을 관리해주므로 version을 명시 하지 않아도 된다.

2. 버전 관리 안해주는 의존성 추가 
https://mvnrepository.com/

mvnrepository 에서 검색

<!-- https://mvnrepository.com/artifact/org.modelmapper/modelmapper -->
<dependency>
    <groupId>org.modelmapper</groupId>
    <artifactId>modelmapper</artifactId>
    <version>2.3.2</version>
</dependency>

3. 기존 의존성 버전 변경하기

<properties>
    <spring.version>5.1.3.RELEASE</spring.version>
</properties>
