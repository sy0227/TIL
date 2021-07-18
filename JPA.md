# JPA 

### JPA란? (Java Persistent API)
- Java ORM 기술에 대한 표준 명세로, JAVA에서 제공하는 API로, 관계형 데이터베이스를 사용하는 방식을 정의한 인터페이스이다. 
- ORM이기 때문에 자바 클래스와 DB 테이블을 매핑한다. (SQL을 매핑하지 않는다.)

### ORM이란? (SQL Mapper & ORM)
- ORM은 DB 테이블을 자바 객체로 매핑하여 객체 간의 관계를 바탕으로 SQL을 자동으로 생성해준다. (Mapper는 SQL을 명시해주어야 한다.)
- ORM은 RDB의 관계를 Object에 반영하는 것이 목적이라면, Mapper는 단순히 필드를 매핑시키는 것이 목적이다.
##### 1) SQL Mapper
* SQL문으로 직접 DB를 조작
* MyBatis, JDBCTemplate
##### 2) ORM (Object-Relation Mapping)
*  객체를 통해 간접적으로 DB를 다룬다
* 객체와 DB의 데이터를 자동으로 매핑해준다.
	* SQL 쿼리가 아니라 메서드로 데이터를 조작할 수 있다.
	* 객체 간 관계를 바탕으로 SQL을 자동으로 생성한다.
- JPA, Hibernate

### JPA 동작 과정
JPA는 애플리케이션과 JDBC 사이에서 동작한다.
개발자가 JPA를 사용하면, JPA 내부에서 JDBC API를 사용하여 SQL을 호출하여 DB와 통신한다. 즉, 개발자가 직접 JDBC API를 쓰는 것이 아니다.
#### INSERT
![INSERT img](https://media.vlpt.us/images/adam2/post/4c17dbbd-79d3-4728-9d8c-83b64a602303/Untitled%204.png)
MemberDAO에서 객체를 저장하고 싶을 때 개발자는 JPA에 Member 객체를 넘긴다.
JPA는
1. Member 엔티티를 분석한다.
2. INSERT SQL을 생성한다.
3. JDBC API를 사용하여 SQL을 DB에 날린다.
#### FIND
![FIND img](https://media.vlpt.us/images/adam2/post/b579405a-fca9-4925-a418-1f2bcac68597/Untitled%205.png)
개발자는 member의 pk값을 JPA에 넘긴다.
JPA는
1. 엔티티의 매핑 정보를 바탕으로 적절한 SELECT SQL을 생성한다.
2.  JDBC API를 사용하여 SQL을 DB에 날린다.
3.  DB로부터 결과를 받아온다.
4.  결과(ResultSet)를 객체에 모두 매핑한다.  
    쿼리를 JPA가 만들어 주기 때문에 Object와 RDB 간의 패러다임 불일치를 해결할 수 있다.
    
### JPA의 특징
- 데이터를 객체지향적으로 관리할 수 있기 때문에 개발자는 비즈니스 로직에 집중할 수 있고 객체지향 개발이 가능하다.
-  자바 객체와 DB 테이블 사이의 매핑 설정을 통해 SQL을 생성한다.
- 객체를 통해 쿼리를 작성할 수 있는 JPQL(Java Persistence Query Language)를 지원
- JPA는 성능 향상을 위해 지연 로딩이나 즉시 로딩과 같은 몇가지 기법을 제공하는데 이것을 잘 활용하면 SQL을 직접 사용하는 것과 유사한 성능을 얻을 수 있다.
- 
### JPA를 왜 사용해야 할까?
- SQL 중심적인 개발에서 객체 중심적인 개발이 가능하다.
	- SQL 코드의 반복, 객체지향과 관계지향 데이터베이스의 패러다임 불일치
	- 기존에는 SQL Mapper 작업을 너무 많이 함
- 생산성이 증가한다.
	- 간단한 메소드로 CRUD가 가능
- 유지보수가 쉽다
	- 필드만 추가하면 된다. SQL은 JPA가 처리하기 때문에 손댈 것이 없다.
- Object와 RDB 간의 패러다임 불일치 해결

### JPA Hibernate
하이버네이트는 JPA 구현체의 한 종류이다.
JPA는 DB와 자바 객체를 매핑하기 위한 인터페이스(API)를 제공하고 JPA 구현체(Hibernate)는 이 인터페이스를 구현한 것이다.
- Hibernate가 SQL을 직접 사용하지 않는다고 해서 JDBC API를 사용하지 않는다는 것은 아니다.
	- Hibernate가 지원하는 메서드 내부에서는 JDBC API가 동ㅈ가하고 있으며, 단지 개발자가 직접 SQL을 직접 작성하지 않을 뿐이다.
- HQL(Hibernate Query Language)이라 불리는 강력한 쿼리 언어를 포함하고 있다.

### JPA에서의 영속성
JPA의 핵심 내용은 엔티티가 영속성 컨텍스트에 포함되어 있냐 아니냐로 갈린다. JPA의 엔티티 매니저가 활성화된 상태로 트랜잭션(@Transactional) 안에서 DB에서 데이터를 가져오면 이 데이터는 영속성 컨텍스트가 유지된 상태이다. 이 상태에서 해당 데이터 값을 변경하면 트랜잭션이 끝나는 시점에 해당 테이블에 변경 내용을 반영하게 된다. 따라서 우리는 엔티티 객체의 필드 값만 변경해주면 별도로 update()쿼리를 날릴 필요가 없게 된다.

##### 출처
[velog - JPA는 도대체 뭘까?](https://velog.io/@adam2/JPA%EB%8A%94-%EB%8F%84%EB%8D%B0%EC%B2%B4-%EB%AD%98%EA%B9%8C-orm-%EC%98%81%EC%86%8D%EC%84%B1-hibernate-spring-data-jpa)
