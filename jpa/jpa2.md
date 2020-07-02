# 엔티티맵핑
## @Entity
- 테이블과 맵핑할 클래스
- 기본생성자 필수

## @Table
- 엔티티와 매핑할 테이블과 맵핑
- 주요속성
  - name: 테이블명
  - uniqueConstraints: 유니크 제약조건
    ```java
    uniqueConstraints = {
      @UniqueConstraint 
    }
    ```
  - indexes: 인덱스를 설정
    ```java
    indexes = {
      @Index(name="NSF_UPLOADED_FILE_MIG_IDX1", columnList="fileName"),
      @Index(name="IDX_NSF_UPLOADED_FILE_MIG_2", columnList="filePath, realFileName"),
      @Index(name="IDX_NSF_UPLOADED_FILE_3", columnList="fileId"),
      @Index(name="IDX_NSF_UPLOADED_FILE_4", columnList="realFileName")
    }
    ```
## @Id
```java
@Id
@GeneratedValue(stragtegy = GenerationType.AUTO)
private Long id;
```
### 기본키 할당
1. IDENTITY
  - MySql, PostgreSQL, SQL Server, DB2
  - MySql은 AUTO_INCREMENT
```java
  @Id
  @GeneratedValue(strategy = GenerationType.IDENTITY)
  private Long id
```
2. SEQUENCE
```java
  @Entity
  @SequenceGenerator (
    name = "MY_SEQ_GENERATOR",
    sequenceName = "MY_SEQ",
    initialValue = 1, allocationSize = 1)
  public class MySample {
    @Id
    @GeneratedValue(strategy = GenerationType.SEQUENCE, generator = "MY_SEQ_GENERATOR")
    private Long id;
  }
```
*** allocationSize 기본값 50이므로 1씩 증가해야한다면 1로 설정해야함

- 아래와 같이 GeneratedValue와 같이 사용해도 됨
```java
  @Id
  @GeneratedValue(strategy = GenerationType.SEQUENCE, generator = "MY_SEQ_GENERATOR")
  @SequenceGenerator (name = "MY_SEQ_GENERATOR", sequenceName = "MY_SEQ", initialValue = 1, allocationSize = 1)
  private Long id;
```
3. TABLE
- 테이블로 시퀀스 흉내내는 방법
- allocationSize 기본값 50
- 
```java
  @Entity
  @TableGenerator (
    name = "MY_SEQ_GENERATOR",
    table = "MY_SEQ_TB",
    pkColumnValue = "MY_SEQ" = 1, 
    initialValue = 1,
    allocationSize = 1)
  public class MySample {
    @Id
    @GeneratedValue(strategy = GenerationType.TABLE, generator = "MY_SEQ_GENERATOR")
    private Long id;
  }
```
4. AUTO
- IDENTITY OR SEQUENCE, TABLE 중에 하나를 자동으로 선택
- ORACLE -> SEQUENCE
- MYSQL -> IDENTITY
### 복합키
1. @IdClass
```java
 class MyPK implements Serializable {
   private int myNo;
   private String myKey;
 }

 @Entity
 @IdClass(MyPK.class)
 class MyProfile {
   @Id
   private int myNo;

   @Id
   private String myKey;
 }
```
2. @EmbeddedId
```java
@Embeddable
class MyId implements Serializable {
  private int myNo;
  private String myKey;
}

@Entity
class MyProfile {
  @EmbeddedId
  private MyId myId;
  private String name;
  private int age;
}
```

### @Column
1. name
2. nullable
3. unique
4. columnDefinition
5. length
6. precision, scale
```java
  @Column(name = "NAME", length=20, unique = true, nullable = false)
  private String name;
  @Column(precision = 19, scale = 2)
  private BigDecimal bigNumber;
  @Column(columnDefinition = "varchar(200) default 'ABC'")
  private String colExampleDefaultAbc

```
### @Enumerated
```java
@Enumerated(EnumType.ORDINAL)
private SampleEnumType sampleType;

@Enumerated(EnumType.STRING)
private RoleType roleType;
```
### @Temporal
- java.util.Date or java.util.Calendar
```java
@Temporal(TemporalType.DATE)
private Date date;
@Temporal(TemporalType.TIME)
private Date time;
@Temporal(TemporalType.TIMESTAMP)
private Date timestamp;
```
### @Lob
BLOB, CLOB 타입으로 저장
1. 문자인 경우 CLOB
2. 나머지 타입인 경우 BLOB
```java
@Lob
private String str;

@Lob
private byte[] byteToBlob;
```
### @Transient
저장 조회 되지 않도록 설정
### @Access

### Auditing
```java
@MappedSuperclass
@EntityListeners(value = {AuditingEntityListener.class})
@Getter
public abstract class AuditorEntity {

	@CreatedDate
	private LocalDateTime createdAt;

	@LastModifiedDate
	private LocalDateTime lastModifiedAt;

	@CreatedBy
	private String createdBy;

	@LastModifiedBy
	private String lastModifiedBy;

}
```