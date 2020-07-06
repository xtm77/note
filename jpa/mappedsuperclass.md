# MappedSuperclass
+ 공통 매핑 정보가 필요할 때 사용
+ 공통 속성 상속
```java
@MappedSuperclass
public abstract BaseEntity {
  
  private LocalDateTime createdAt;
  private LocalDateTime lastModifiedAt;

  private String createdBy;
  private String lastModifedBy;
}
```

+ 상속관계매핑아님
+ 엔티티 아님
+ 테이블과 매핑 아님
+ 부모클래스를 상속받는 자식 클르스에 매핑 정보만 제공
+ 조회, 검색 불가
+ 직접생성해서 사용할일이 없으므로 추상클래스 권장
