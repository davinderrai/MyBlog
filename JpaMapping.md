#### JPA Mappings

##### One to One Mapping Unidirectional

###### Customer Entity
```java
@Entity
public @Data
class Customer {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Integer id;

    private String name;

    @OneToOne
    private Shipping shippingaddr;
}
```

###### Shipping Entity
```java
@Entity
public @Data class Shipping {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Integer id;

    private String name;

    private String city;
}
```
