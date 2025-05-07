# Spring Data JPA Order Service

This repository contains source code examples to support my course [Spring Data JPA and Hibernate Beginner to Guru](https://www.udemy.com/course/hibernate-and-spring-data-jpa-beginner-to-guru/?referralCode=251C4C865302C7B1BB8F)

## Connect with Spring Framework Guru
* Spring Framework Guru [Blog](https://springframework.guru/)
* Subscribe to Spring Framework Guru on [YouTube](https://www.youtube.com/channel/UCrXb8NaMPQCQkT8yMP_hSkw)
* Like Spring Framework Guru on [Facebook](https://www.facebook.com/springframeworkguru/)
* Follow Spring Framework Guru on [Twitter](https://twitter.com/spring_guru)
* Connect with John Thompson on [LinkedIn](http://www.linkedin.com/in/springguru)

```
create table order_approval
(
    id                 bigint not null auto_increment primary key,
    approved_by        varchar(50),
    created_date       timestamp,
    last_modified_date timestamp
);

alter table order_header
    add column order_approval_id bigint;

alter table order_header
    add constraint order_approval_fk
        foreign key (order_approval_id) references order_approval (id);
-------------------
@Entity
public class OrderApproval extends BaseEntity {

    private String approvedBy;
-----------------------
public class OrderHeader extends BaseEntity {
@OneToOne
    private OrderApproval orderApproval;
------------------------
public interface OrderApprovalRepository extends JpaRepository<OrderApproval, Long> {
}
------------------------
@Test
    void testSaveOrderWithLine() {
        OrderHeader orderHeader = new OrderHeader();
        Customer customer = new Customer();
        customer.setCustomerName("New Customer");
        Customer savedCustomer = customerRepository.save(customer);

        orderHeader.setCustomer(savedCustomer);

        OrderLine orderLine = new OrderLine();
        orderLine.setQuantityOrdered(5);
        orderLine.setProduct(product);

        orderHeader.addOrderLine(orderLine);

        OrderApproval approval = new OrderApproval();
        approval.setApprovedBy("me");
        OrderApproval savedApproval = orderApprovalRepository.save(approval);
        orderHeader.setOrderApproval(savedApproval);

        OrderHeader savedOrder = orderHeaderRepository.save(orderHeader);

```