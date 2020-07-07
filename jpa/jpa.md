# JPA
1. JPA란?
  - JDBC -> MyBatis, JdbcTemplate -> JPA
  - JPA가 적절한 SQL 생성
  - 개발생산성 및 유지보수의 효율성
2. JPA 실무에서 어려운 이유 -> 복잡한 실무 상황에 맞는 객체 설계 방법이 필요
  - 처음 JPA나 스프링 데이터 JPA를 만나면
  - SQL 자동화, 수집줄의 코드가 한 두줄로!
  - 실무에 바로 도입?
  - 예제들은 보통 테이블이 한 두개로 단순
  - 실무는 수십 개 이상의 복잡한 객체와 테이블 사용
  - JPA 내부 동작 방식을 알아야 한다.


3. SQL 중심적인 개발의 문제점
- 아직은 관계형 DB가 중심
- 객체를 관계형 DB에 저장해야 함.(언어를 객체지향언어)
- 객체를 SQL로 변환, CRUD의 무한반복
- 필드가 하나 추가되었을 때 해야할 일들...
  - CRUD쿼리 모두 수정(insert, select, update sql 필드 추가)
  - 나중에 빠진 쿼리가 발생할 수 있음.
4. 패러다임의 불일치(객체vs관계형DB)
- 객체지향프로그래밍 - 추상화, 캡슐화, 정보은닉, 상속, 다형성
- 객체 ---> RDB  
       ---> NoSQL  
       ---> File  
       ---> OODB  
- 객체 -> SQL변환 -> RDB (개발자 = SQL 맵퍼)
6. 차이
- 상속: 객체(O), RDB(X)
- 연관관계: 객체(O), RDB(O)

7. 객체의 상속관계
- RDB의 테이블 슈퍼타입 서브타입 관계
![객체상속](./images/클래스다이어그램_상속.png)

8. 연관관계
- 테이블은 양방향으로 서로 찾을 수 있다.
- 객체는 방향이 있다.

```java
class Member {
  String id;
  Team team;
  String username;
}

class Team {
  Long id;
  String teamName;
}
```
```sql
SELECT M.*, T.*
FROM MEMBER M
JOIN TEAM T
ON T.TEAM_ID = M.TEAM_ID
```


1980년도 부터 객체

ORM
- object-relational mapping(객체맵핑관계)
- 객체는 객체대로 설계
- 관계형 DB는 관계형 데이터베이스 대로 설계
- orm 프레임워크가 중간에서 맵핑

jpa 구조
java -> jpa -> jdbc api -> sql -> db

- sql 생성
- jdbc api 사용
- resultset 맵핑
- 패러다임 불일치 해결

jpa 인터페이스 모음, 스펙
실제 구현체는 하이버네이트, 이클립스링크등.. 주로 하이버네이트

사용하는 이유
- sql 중심 개발 -> 객체 중심 개발
- 생산성
- 유지보수
- 패러다임 불일치 해결
- 성능
- 데이터 접근 추상화와 벤더 독립성
- 표준

객체 그래프 탐색


지연로딩과 즉시로딩

## spring data jpa
spring data jpa는 jpa 기반 레포지토리를 쉽게 구현하는 것을 쉽게 만들어 줌  
jpa 기반 데이터 접근 레이어를 위한 향상된 지원  
데이터 접근 기술들을 이용한 강력한 스프링 애플리케이션을 더 쉽게 구축  

- spring data jpa는 transactionManager라는 명명된 PlatformTransactionManager bean이 필요함
- annotaion-based 설정
```java
@Configuration
@EnableJpaRepositories
@EnableTransactionManagement
class ApplicationConfig {
  @Bean
  public DataSource dataSource() {

  }
}
```


## 자연키 인조키
- 자연키 : 비지니스 모델에서 나오는 키 (TicketNo, 이메일주소등)
- 인조키(대리키) : 데이터 측면에서 만들어내는 키(시퀀스)




## 엔티티 생명주기
- 비영속성(new/transient)
- 영속(managed)
- 준영속(detached)
- 삭제(removed)

## JPA 기본 페치 전략
- @ManyToOne, @OneToOne: 즉시로딩(FetchType.EAGER)
- @OneToMany, @ManyToMany: 지연로딩(FetchType.LAZY)



