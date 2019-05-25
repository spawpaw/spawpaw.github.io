---
layout: post
title:  "Spring Data JPA 二：实体的定义"
date:   2018-05-14 13:50:40 +0800
categories: spring
tags: spring-data-jpa hibernate
---

## 简单的例子
以下两个类分别定义了`User`和`Article`两个对象，每个用户拥有多个Article，每个article只有一个作者(user)

### 实体类：User
```java
@Entity 
@Table(name = "user") 
public class User implements Serializable {
    @Id
    @Column(name = "id")
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id; 
    
    @Basic
    @Column(name = "username")
    private String username; 
    
    @Basic
    @Column(name = "password")
    private String password;
    
    @ManyToOne(mappedBy="author")
    Set<Article> articles;
    
    // 此处省略 getter 和 setter 。
}
```

### 实体类：Article
```java
@Entity 
@Table(name = "article") 
public class Article implements Serializable { 
    @Id
    @Column(name = "id")
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id; 
    
    @Basic
    @Column(name = "content")
    private String content; 
    
    @OneToMany
    @JoinColumn(name = "author_id")
    private User author;
 
    // 此处省略 getter 和 setter 。
}
```

### DAO
```java
//User类的DAO：
public interface UserRepository extends JpaRepository<Privilege, Integer>  {
}

//Article的DAO：
public interface ArticleRepository extends JpaRepository<Privilege, Integer>  {
}
```

### 使用：
```java
public class UserService{
    @Resource
    UserRepository userRepository;
    
    List<User> getUserList(){
        return userRepository.findAll();
    }
    
    List<Article> getArticleListByUserId(Long userId){
        return userRepository.getOne(userId).getArticles();
    }
    
}

```
## 几个注解

### 实体
#### @Entity
#### @Table(name = "t")
#### @Table(name = "t")
 
 ### 属性
 
 #### Id
 
 #### Column
 
 #### Basic
 
 ### 关系
 
 #### OneToOne
 
 #### OneToMany
 
 #### ManyToOne
 
 #### ManyToMany
 
 #### JoinTable
 






## 参考文档
> [Spring Data JPA 官方文档](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/)