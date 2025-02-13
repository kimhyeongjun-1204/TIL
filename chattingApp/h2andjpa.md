## 💡H2 데이터베이스와 JPA 연동하기 

## 🌟application.properties 환경 설정 

### 1️⃣H2 데이터베이스 설정 
```properties

spring.datasource.driver-class-name=org.h2.Driver
spring.datasource.url=jdbc:h2:mem:test   # H2 DB 연결 주소 (In-Memory Mode : 휘발성 )
# spring.datasource.url=jdbc:h2:~/test   # H2 DB 연결 주소 (Embedded Mode)
spring.datasource.username=username      # H2 DB 접속 ID (사용자 지정)
spring.datasource.password=password      # H2 DB 접속 PW (사용자 지정)

```

### 🔹 spring.datasource.driver-class-name : h2 데이터베이스의 JDBC 드라이버 클래스를 설정. org.h2.Driver는 h2 데이터베이스를 위한 JDBC 드라이버 클래스 
### 🔹spring.datasource.url : 데이터베이스의 연결 URL을 설정. jdbc:h2:mem:test는 H2의 인메모리 모드(메모리에서만 실행되는 데이터베이스)를 사용하도록 설정
### 🔹spring.datasource.username, password

### 2️⃣ H2 콘솔 설정 

```properties

# H2 Console 설정
spring.h2.console.enabled=true           # H2 Console 사용 여부
spring.h2.console.path=/h2-console       # H2 Console 접속 주소
``` 

### H2 데이터베이스의 웹 기반 콘솔을 사용할 수 있도록 하는 설정 

### 3️⃣ JPA 설정 
```properties
# JPA 설정
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
spring.jpa.hibernate.ddl-auto=create    # DB 초기화 전략 (none, create, create-drop, update, validate)
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.H2Dialect
spring.jpa.properties.hibernate.format_sql=true   # 쿼리 로그 포맷 (정렬)
spring.jpa.properties.hibernate.show_sql=true     # 쿼리 로그 출력
```

🔹 spring.jpa.database-platform : JPA에서 사용할 데이터베이스 플랫폼. org.hibernate.dialect.H2Dialect는 Hibernate 가 H2 데이터베이스에 맞게 SQL 쿼리를 생성할 수 있게 함 

🔹 **spring.jpa.hibernate.ddl-auto** : DDL 자동 생성 옵션. 애플리케이션 실행시 테이블을 삭제하고 새로 생성할 것인지, 새로 생성된 필드만 추가할 것인지 등을 결정함. 

### 테이블 생성 전략 
![alt text]({A6F115F8-DF27-410E-890B-91A013FA7EB4}.png)

🔹 밑 3줄 : Hiberate가 실행하는 SQL 쿼리를 로그에 출력하게 설정함. 

> 💡Hibernate란? : JPA의 구현체로 
> 
![alt text]({C6B73E99-04C4-4914-98F3-10488E430E7D}.png)


## 🌟h2 DB의 In-Memory 모드로 설정된 테이블을 H2 콘솔을 이용하여 확인하기  

### 1️⃣ application.properties 파일에서 H2 콘솔 활성화
```properties
spring.h2.console.enabled=true
spring.h2.console.path=/h2-console
``` 
#### ✔️ 콘솔 활성화 및 경로 설정함(/h2-console). 

### 2️⃣ 애플리케이션 실행 후 브라우저에서 H2 콘솔 열기
<br/>

> URL: http://localhost:8080/h2-console
>
> 데이터베이스 URL: jdbc:h2:mem:test (기본 설정)
> 
> 사용자명과 비밀번호는 application.properties에 설정한 값


### 3️⃣ 로그인 후 테이블 확인
<br/>

> H2 콘솔에 접속하여, RUN SCRIPT 또는 SELECT * FROM <테이블명> 등의 SQL 명령어로 데이터베이스 테이블을 확인
