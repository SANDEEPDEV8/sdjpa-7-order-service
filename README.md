# Spring Data JPA Order Service

This repository contains source code examples to support my course [Spring Data JPA and Hibernate Beginner to Guru](https://www.udemy.com/course/hibernate-and-spring-data-jpa-beginner-to-guru/?referralCode=251C4C865302C7B1BB8F)

## Connect with Spring Framework Guru
* Spring Framework Guru [Blog](https://springframework.guru/)
* Subscribe to Spring Framework Guru on [YouTube](https://www.youtube.com/channel/UCrXb8NaMPQCQkT8yMP_hSkw)
* Like Spring Framework Guru on [Facebook](https://www.facebook.com/springframeworkguru/)
* Follow Spring Framework Guru on [Twitter](https://twitter.com/spring_guru)
* Connect with John Thompson on [LinkedIn](http://www.linkedin.com/in/springguru)

one to one bidirectional with foreign key
```
alter table order_approval
    add column order_header_id bigint;

alter table order_approval
    add constraint order_hdr_fk
        foreign key (order_header_id) references order_header (id);
```

```
@Entity
public class OrderApproval extends BaseEntity {

    @OneToOne
    @JoinColumn(name = "order_header_id")
    private OrderHeader orderHeader;


public class OrderHeader extends BaseEntity {


    @OneToOne(cascade = {CascadeType.PERSIST, CascadeType.REMOVE}, mappedBy = "orderHeader")
    private OrderApproval orderApproval;

    public void setOrderApproval(OrderApproval orderApproval) {
        this.orderApproval = orderApproval;
        orderApproval.setOrderHeader(this);
    }
```

when order header is delted it thows error sue to foreign key, so keep CascadeType.REMOVE