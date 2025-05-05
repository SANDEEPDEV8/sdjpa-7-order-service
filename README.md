# Spring Data JPA Order Service

This repository contains source code examples to support my course [Spring Data JPA and Hibernate Beginner to Guru](https://www.udemy.com/course/hibernate-and-spring-data-jpa-beginner-to-guru/?referralCode=251C4C865302C7B1BB8F)

## Connect with Spring Framework Guru
* Spring Framework Guru [Blog](https://springframework.guru/)
* Subscribe to Spring Framework Guru on [YouTube](https://www.youtube.com/channel/UCrXb8NaMPQCQkT8yMP_hSkw)
* Like Spring Framework Guru on [Facebook](https://www.facebook.com/springframeworkguru/)
* Follow Spring Framework Guru on [Twitter](https://twitter.com/spring_guru)
* Connect with John Thompson on [LinkedIn](http://www.linkedin.com/in/springguru)

```
create table category (
      id bigint not null auto_increment primary key,
      description varchar(50),
      created_date timestamp,
      last_modified_date timestamp
);

create table product_category (
      product_id bigint not null,
      category_id bigint not null,
      primary key (product_id, category_id),
      constraint pc_product_id_fk FOREIGN KEY (product_id) references product(id),
      constraint pc_category_id_fk FOREIGN KEY (category_id) references category(id)
);
--------------------------

@Entity
public class Product extends BaseEntity {

    @ManyToMany
    @JoinTable(name = "product_category",
        joinColumns = @JoinColumn(name = "product_id"),
        inverseJoinColumns = @JoinColumn(name = "category_id"))
    private Set<Category> categories;
------------------
public interface ProductRepository extends JpaRepository<Product, Long> {

    Product findByDescription(String description);
}
----------------
 @Test
    void testGetCategory() {
        Product product = productRepository.findByDescription("PRODUCT1");

        assertNotNull(product);
        assertNotNull(product.getCategories());

    }


```