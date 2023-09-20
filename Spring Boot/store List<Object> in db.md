
@ElementCollection @CollectionTable @Embeddable


```java
@Entity
public class Employee {
  @Id
  @Column(name="EMP_ID")
  private long id;
  ...
  @ElementCollection
  @CollectionTable(
        name="PHONE",
        joinColumns=@JoinColumn(name="OWNER_ID")
  )
  private List<Phone> phones;
  ...
}
```


```java
@Embeddable
public class Phone {
  private String type;
  private String areaCode;
  @Column(name="P_NUMBER")
  private String number;
  ...
}
```

##Example of a ElementCollection relationship to a basic value annotations
```java
@Entity
public class Employee {
  @Id
  @Column(name="EMP_ID")
  private long id;
  ...
  @ElementCollection
  @CollectionTable(
        name="PHONE",
        joinColumns=@JoinColumn(name="OWNER_ID")
  )
  @Column(name="PHONE_NUMBER")
  private List<String> phones;
  ...
}

```


![[Pasted image 20230912005548.png]]