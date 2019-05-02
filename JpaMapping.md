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

Will Result in
```sql
Hibernate: create table customer (id integer not null auto_increment, name varchar(255), shippingaddr_id integer, primary key (id)) engine=MyISAM
Hibernate: create table shipping (id integer not null auto_increment, city varchar(255), name varchar(255), primary key (id)) engine=MyISAM
Hibernate: alter table customer add constraint FKcx1tx3u33gi3o4ul0wb4b5pqd foreign key (shippingaddr_id) references shipping (id)
```

##### One to One Mapping Unidirectional with @JoinColumn

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
    @JoinColumn(name="address_id")
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

Will Result in
```sql
Hibernate: create table customer (id integer not null auto_increment, name varchar(255), address_id integer, primary key (id)) engine=MyISAM
Hibernate: create table shipping (id integer not null auto_increment, city varchar(255), name varchar(255), primary key (id)) engine=MyISAM
Hibernate: alter table customer add constraint FKmtcudeswxbsgplh2sr43jjujn foreign key (address_id) references shipping (id)
```
