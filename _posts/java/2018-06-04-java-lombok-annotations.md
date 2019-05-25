---
layout: post
title: "Lombok-注解"
date:   2018-07-15 11:23:00 +0800
categories: java
tags: lombok
---

## Lombok Annotations
It is not uncommon for a typical Java project to devote hundreds of lines of code to the boilerplate required for defining simple data classes. These classes generally contain a number of fields, getters and setters for those fields, as well as equals and hashCode implementations. In the simplest scenarios, Project Lombok can reduce these classes to the required fields and a single @Data annotation.

Of course, the simplest scenarios are not necessarily the ones that developers face on a day-to-day basis. For that reason, there are a number of annotations in Project Lombok to allow for more fine grained control over the structure and behavior of a class.

### @Getter and @Setter
The @Getter and @Setter annotations generate a getter and setter for a field, respectively. The getters generated correctly follow convention for boolean properties, resulting in an isFoo getter method name instead of getFoo for any boolean field foo. It should be noted that if the class to which the annotated field belongs contains a method of the same name as the getter or setter to be generated, regardless of parameter or return types, no corresponding method will be generated.

Both the @Getter and @Setter annotations take an optional parameter to specify the access level for the generated method.

Lombok annotated code:

```java
@Getter @Setter private boolean employed = true;
@Setter(AccessLevel.PROTECTED) private String name;
```
Equivalent Java source code:
```java
private boolean employed = true;
private String name;

public boolean isEmployed() {
    return employed;
}

public void setEmployed(final boolean employed) {
    this.employed = employed;
}

protected void setName(final String name) {
    this.name = name;
}
```

### @NonNull
The @NonNull annotation is used to indicate the need for a fast-fail null check on the corresponding member. When placed on a field for which Lombok is generating a setter method, a null check will be generated that will result in a NullPointerException should a null value be provided. Additionally, if Lombok is generating a constructor for the owning class then the field will be added to the constructor signature and the null check will be included in the generated constructor code.

This annotation mirrors @NotNull and @NonNull annotations found in IntelliJ IDEA and FindBugs, among others. Lombok is annotation agnostic with regards to these variations on the theme. If Lombok comes across any member annotated with any annotation of the name @NotNull or @NonNull, it will honor it by generating the appropriate corresponding code. The authors of Project Lombok further comment that, in the event that annotation of this type is added to Java, then the Lombok version will be subject to removal.

Lombok annotated code from the class Family:
```java
@Getter @Setter @NonNull
private List<Person> members;
```

Equivalent Java source code:
```java
@NonNull
private List<Person> members;

public Family(@NonNull final List<Person> members) {
    if (members == null) throw new java.lang.NullPointerException("members");
    this.members = members;
}
    
@NonNull
public List<Person> getMembers() {
    return members;
}

public void setMembers(@NonNull final List<Person> members) {
    if (members == null) throw new java.lang.NullPointerException("members");
    this.members = members;
}
```


### @ToString
This annotation generates an implementation of the toString method. By default, any non-static fields will be included in the output of the method in name-value pairs. If desired, the inclusion of the property names in the output can be suppressed by setting the annotation parameter includeFieldNames to false.

Specific fields can be excluded from the output of the generated method by including their field names in the exclude parameter. Alternatively, the of parameter can be used to list only those fields which are desired in the output. The output of the toString method of a superclass can also be included by setting the callSuper parameter to true.

Lombok annotated code:
```java
@ToString(callSuper=true,exclude="someExcludedField")
public class Foo extends Bar {
    private boolean someBoolean = true;
    private String someStringField;
    private float someExcludedField;
}
```
Equivalent Java source code:
```java
public class Foo extends Bar {
    private boolean someBoolean = true;
    private String someStringField;
    private float someExcludedField;
    
    @java.lang.Override
    public java.lang.String toString() {
        return "Foo(super=" + super.toString() +
            ", someBoolean=" + someBoolean +
            ", someStringField=" + someStringField + ")";
    }
}
```

### @EqualsAndHashCode
This class level annotation will cause Lombok to generate both equals and hashCode methods, as the two are tied together intrinsically by the hashCode contract. By default, any field in the class that is not static or transient will be considered by both methods. Much like @ToString, the exclude parameter is provided to prevent field from being included in the generated logic. One can also use the of parameter to list only those fields should be considered.

Also like @ToString, there is a callSuper parameter for this annotation. Setting it to true will cause equals to verify equality by calling the equals from the superclass before considering fields in the current class. For the hashCode method, it results in the incorporation of the results of the superclass's hashCode in the calculation of the hash. When setting callSuper to true, be careful to make sure that the equals method in the parent class properly handles instance type checking. If the parent class checks that the class is of a specific type and not merely that the classes of the two objects are the same, this can result in undesired results. If the superclass is using a Lombok generated equals method, this is not an issue. However, other implementations may not handle this situation correctly. Also note that setting callSuper to true cannot be done when the class only extends Object, as it would result in an instance equality check that short-circuits the comparison of fields. This is due to the generated method calling the equals implementation on Object, which returns false if the two instances being compared are not the same instance. As a result, Lombok will generate a compile time error in this situation.

Lombok annotated code:
```java
@EqualsAndHashCode(callSuper=true,exclude={"address","city","state","zip"})
public class Person extends SentientBeing {
    enum Gender { Male, Female }

    @NonNull private String name;
    @NonNull private Gender gender;
    
    private String ssn;
    private String address;
    private String city;
    private String state;
    private String zip;
}
```
Equivalent Java source code:
```java
public class Person extends SentientBeing {
    
    enum Gender {
        /*public static final*/ Male /* = new Gender() */,
        /*public static final*/ Female /* = new Gender() */;
    }
    @NonNull
    private String name;
    @NonNull
    private Gender gender;
    private String ssn;
    private String address;
    private String city;
    private String state;
    private String zip;
    
    @java.lang.Override
    public boolean equals(final java.lang.Object o) {
        if (o == this) return true;
        if (o == null) return false;
        if (o.getClass() != this.getClass()) return false;
        if (!super.equals(o)) return false;
        final Person other = (Person)o;
        if (this.name == null ? other.name != null : !this.name.equals(other.name)) return false;
        if (this.gender == null ? other.gender != null : !this.gender.equals(other.gender)) return false;
        if (this.ssn == null ? other.ssn != null : !this.ssn.equals(other.ssn)) return false;
        return true;
    }
    
    @java.lang.Override
    public int hashCode() {
        final int PRIME = 31;
        int result = 1;
        result = result * PRIME + super.hashCode();
        result = result * PRIME + (this.name == null ? 0 : this.name.hashCode());
        result = result * PRIME + (this.gender == null ? 0 : this.gender.hashCode());
        result = result * PRIME + (this.ssn == null ? 0 : this.ssn.hashCode());
        return result;
    }
}
```

### @Data
The @Data annotation is likely the most frequently used annotation in the Project Lombok toolset. It combines the functionality of @ToString, @EqualsAndHashCode, @Getter and @Setter. Essentially, using @Data on a class is the same as annotating the class with a default @ToString and @EqualsAndHashCode as well as annotating each field with both @Getter and @Setter. Annotation a class with @Data also triggers Lombok's constructor generation. This adds a public constructor that takes any @NonNull or final fields as parameters. This provides everything needed for a Plain Old Java Object (POJO).

While @Data is extremely useful, it does not provide the same granularity of control as the other Lombok annotations. In order to override the default method generation behaviors, annotate the class, field or method with one of the other Lombok annotations and specify the necessary parameter values to achieve the desired effect.

@Data does provide a single parameter option that can be used to generate a static factory method. Setting the value of the staticConstructor parameter to the desired method name will cause Lombok to make the generated constructor private and expose a a static factory method of the given name.

Lombok annotated code:
```java
@Data(staticConstructor="of")
public class Company {
    private final Person founder;
    private String name;
    private List<Person> employees;
}
```

Equivalent Java source code:
```java
public class Company {
    private final Person founder;
    private String name;
    private List<Person> employees;
    
    private Company(final Person founder) {
        this.founder = founder;
    }
    
    public static Company of(final Person founder) {
        return new Company(founder);
    }
    
    public Person getFounder() {
        return founder;
    }
    
    public String getName() {
        return name;
    }
    
    public void setName(final String name) {
        this.name = name;
    }
    
    public List<Person> getEmployees() {
        return employees;
    }
    
    public void setEmployees(final List<Person> employees) {
        this.employees = employees;
    }
    
    @java.lang.Override
    public boolean equals(final java.lang.Object o) {
        if (o == this) return true;
        if (o == null) return false;
        if (o.getClass() != this.getClass()) return false;
        final Company other = (Company)o;
        if (this.founder == null ? other.founder != null : !this.founder.equals(other.founder)) return false;
        if (this.name == null ? other.name != null : !this.name.equals(other.name)) return false;
        if (this.employees == null ? other.employees != null : !this.employees.equals(other.employees)) return false;
        return true;
    }
    
    @java.lang.Override
    public int hashCode() {
        final int PRIME = 31;
        int result = 1;
        result = result * PRIME + (this.founder == null ? 0 : this.founder.hashCode());
        result = result * PRIME + (this.name == null ? 0 : this.name.hashCode());
        result = result * PRIME + (this.employees == null ? 0 : this.employees.hashCode());
        return result;
    }
    
    @java.lang.Override
    public java.lang.String toString() {
        return "Company(founder=" + founder + ", name=" + name + ", employees=" + employees + ")";
    }
}
```

### @Cleanup
The @Cleanup annotation can be used to ensure that allocated resources are released. When a local variable is annotated with @Cleanup, any subsequent code is wrapped in a try/finally block that guarantees that the cleanup method is called at the end of the current scope. By default @Cleanup assumes that the cleanup method is named "close", as with input and output streams. However, a different method name can be provided to the annotation's value parameter. Only cleanup methods which take no parameters are able to be used with this annotation.

There is also a caveat to consider when using the @Cleanup annotation. In the event that an exception is thrown by the cleanup method, it will preempt any exception that was thrown in the method body. This can result in the actual cause of an issue being buried and should be considered when choosing to use Project Lombok's resource management. Furthermore, with automatic resource management on the horizon in Java 7, this particular annotation is likely to be relatively short-lived.

Lombok annotated code:
```java
public void testCleanUp() {
    try {
        @Cleanup ByteArrayOutputStream baos = new ByteArrayOutputStream();
        baos.write(new byte[] {'Y','e','s'});
        System.out.println(baos.toString());
    } catch (IOException e) {
        e.printStackTrace();
    }
}
```
Equivalent Java source code:
```java
public void testCleanUp() {
    try {
        ByteArrayOutputStream baos = new ByteArrayOutputStream();
        try {
            baos.write(new byte[]{'Y', 'e', 's'});
            System.out.println(baos.toString());
        } finally {
            baos.close();
        }
    } catch (IOException e) {
        e.printStackTrace();
    }
}
```

### @Synchronized
Using the synchronized keyword on a method can result in unfortunate effects, as any developer who has worked on multi-threaded software can attest. The synchronized keyword will lock on the current object (this) in the case of an instance method or on the class object for a static method. This means that there is the potential for code outside of the control of the developer to lock on the same object, resulting in a deadlock. It is generally advisable to instead lock explicitly on a separate object that is dedicated solely to that purpose and not exposed in such a way as to allow unsolicited locking. Project Lombok provides the @Synchronized annotation for that very purpose.

Annotating an instance method with @Synchronized will prompt Lombok to generate a private locking field named $lock on which the method will lock prior to executing. Similarly, annotating a static method in the same way will generate a private static object named $LOCK for the static method to use in an identical fashion. A different locking object can be specified by providing a field name to the annotation's value parameter. When a field name is provided, the developer must define the property as Lombok will not generate it.

Lombok annotated code:
```java
private DateFormat format = new SimpleDateFormat("MM-dd-YYYY");

@Synchronized
public String synchronizedFormat(Date date) {
    return format.format(date);
}
```
Equivalent Java source code:
```java
private final java.lang.Object $lock = new java.lang.Object[0];
private DateFormat format = new SimpleDateFormat("MM-dd-YYYY");

public String synchronizedFormat(Date date) {
    synchronized ($lock) {
        return format.format(date);
    }
}
```

### @SneakyThrows
@SneakyThrows is probably the Project Lombok annotation with the most detractors, since it is a direct assault on checked exceptions. There is a lot of disagreement with regards to the use of checked exceptions, with a large number of developers holding that they are a failed experiment. These developers will love @SneakyThrows. Those developers on the other side of the checked/unchecked exception fence will most likely view this as hiding potential problems.

Throwing IllegalAccessException would normally generate an "Unhandled exception" error if IllegalAccessException, or some parent class, is not listed in a throws clause:

Screenshot of Eclipse generating an error message regarding unhandled exceptions.
When annotated with @SneakyThrows, the error goes away.

Screenshot of a method annotated with @SneakyThrows and generating no error in Eclipse.
By default, @SneakyThrows will allow any checked exception to be thrown without declaring in the throws clause. This can be limited to a particular set of exceptions by providing an array of throwable classes ( Class<? extends Throwable>) to the value parameter of the annotation.

Lombok annotated code:
```java
@SneakyThrows
public void testSneakyThrows() {
    throw new IllegalAccessException();
}
```
Equivalent Java source code:
```java
public void testSneakyThrows() {
    try {
        throw new IllegalAccessException();
    } catch (java.lang.Throwable $ex) {
        throw lombok.Lombok.sneakyThrow($ex);
    }
}
```
A look at the above code and the signature of Lombok.sneakyThrow(Throwable) would lead most to believe that the exception is being wrapped in a RuntimeException and re-thrown, however this is not the case. The sneakyThrow method will never return normally and will instead throw the provided throwable completely unaltered.