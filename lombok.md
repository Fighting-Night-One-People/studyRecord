# lombok常用注解

### 在pom.xml中引入lombok依赖

```java
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.16</version>
</dependency>
```

### 新建实体类Student

```java
@Getter
@Setter
@ToString
@EqualsAndHashCode
@NoArgsConstructor
@AllArgsConstructor
public class Student {
    private String id;
}
```

## @Getter

自动产生getter方法

```java
public String getId() {
        return id;
    }
```

## @Setter

自动产生setter方法

```java
public void setId(String id) {
        this.id = id;
    }
```

## @ToString

自动重写toString()方法

```java
@Override
public String toString() {
    return "Student{" +
            "id='" + id + '\'' +
            '}';
}
```

## @EqualsAndHashCode

自动重写equals(Object o )和hashCode()方法

```java
@Override
public boolean equals(Object o) {
    if (this == o) return true;
    if (o == null || getClass() != o.getClass()) return false;
    Student student = (Student) o;
    return Objects.equals(id, student.id);
}
@Override
public int hashCode() {
    return Objects.hash(id);
}
```

## @NoArgsConstructor

自动生成无参构造器

```java
public Student() {}
```

## @AllArgsConstructor

生成一个包含所有参数的构造器

```
public Student(String id) {
    this.id = id;
}
```

## @RequiredArgsConstructor

 生成一个包含 "特定参数" 的构造器，特定参数指的是那些有加上 final 修饰词的变量们.同时，若所有变量都正常，没有用final修饰，就会生成一个无参构造器

```java
private final String name;
public Student(String name){
    this.name=name;
}
```

## @Data

该注解是个整合注解，相当于同时加了以下五个注解

* @Getter
* @Setter
* @ToString
* @EqualsAndHashCode
* @RequiredArgsConstructor

## @Value

该注解是个整合注解，但是他会把所有的变量都设成final,同时没有setter方法，其他的与@Data没有区别

* @Getter(没有Setter)
* @ToString
* @EqualsAndHashCode
* @RequiredArgsConstructor

## @Builder

自动生成流式set值写法，抛弃以前需要写一堆setter

- 新写法

  ```java
  @Getter
  @Setter
  @Builder
  class Student{
      private String id;
      private String name;
  }
  public class Main{
      public static void main(String[] args){
  		Student student=Student.builder().id("2020").name("hello").build();
      }
  }
  ```

- 老写法

  ```java
  public class Main{
      public static void main(String[] args){
  		Student student=new Student();
          student.setId("2020");
          student.setName("hello");
      }
  }
  ```

## @Slf4j

自动生成该类的log静态常量，可以直接打印日志，不需要手动new log

- 新写法

  ```java
  @Slf4j
  public class Main{
      public static void main(String[] args){
          log.info("hello");
      }
  }
  ```

- 老写法

    ```java
    public class Main{
        public static final Logger log= LoggerFactory.getLogger(Main.class);
        public static void main(String[] args){
            log.info("hello");
        }
    }
    ```

    

