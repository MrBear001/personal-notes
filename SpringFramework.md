# Spring Framework

---

## 1. Spring Framework 概述

Spring Framework（简称 Spring）是一个开源的 Java 应用程序框架。

它提供了一整套基础设施支持，使开发者可以专注于业务逻辑，而不必过多关注底层技术细节。主要功能包括但不限于 IoC 容器、AOP 面向切面编程、事务管理、Web MVC等等。同时，Spring Framework 采用模块化设计，我们可以根据项目需求选择性地引入所需模块。

## 2. IoC 容器

### 2.1. 什么是 IoC 容器

我们知道，在面向对象编程中，程序的本质就是通过一系列对象的交互来完成某个任务。对象之间往往存在依赖关系，通常我们的做法是直接在对象内部创建它所依赖的对象，但这相当于把依赖对象写死在了这里，对象与对象之间建立了强耦合。

而 Spring 提供了一个 IoC 容器，也叫 Spring 容器。它可以帮助我们统一管理程序中的对象，并根据对象之间的依赖关系通过依赖注入（DI）对它们进行组装。此时，对象对其依赖的控制权就由对象本身转移到了 Spring 容器，这就是 IoC（Inversion of Control，控制反转）名称的由来。一个由 Spring 容器管理的对象也称为 Bean。

### 2.2. Bean 的注册

将对象交给 Spring 容器管理的过程称为 Bean 的注册。Spring 容器需要通过读取一定的配置信息来实现 Bean 的注册，配置信息的形式有多种，通常我们会使用基于注解和 Java 类的形式来实现 Bean 的注册。

1）基于注解注册 Bean：

Spring 提供了以下注解用于将某个类注册为 Bean：

* @Component
* @Controller
* @Service
* @Repository

这些注解本质上没什么不同，只是针对不同领域的类作了语义上的区分。下面是一个基于注解注册 Bean 的示例：

```java
@Component
public class A {
    @Autowired
    private B b;
}

@Component
public class B {
}
```

在类上加上 @Component 注解就可以将该类注册为 Spring 容器中的 Bean，我们还可以通过 @Component 注解的 value 属性手动指定 Bean 的名称，如果不指定，默认就是类名首字母小写。

如果一个 Bean 依赖另一个 Bean，可以通过 @Autowired 注解实现依赖注入。@Autowired 注解默认是根据依赖项的类型进行注入，如果 Spring 容器中该依赖项类型的 Bean 不唯一，则可以配合 @Qualifier 注解实现按 Bean 的名称进行注入，或者在想优先注入的依赖项上加上 @Primary 注解：

```java
@Component
public class A {
    @Autowired
    @Qualifier("b1")
    private B b;
}

@Component
@Primary
public class B {
}
```

此外，@Autowired 注解还支持设置 required 属性来指定某个依赖项是否是必须注入的：

```java
@Component
public class A {
    @Autowired(required = false)
    private B b;
}

@Component
public class B {
}
```

需要注意的是，@Autowired 注解不仅可以加在字段上，还可以加载构造方法或者 setter 方法上，通常我们更建议通过构造函数进行依赖注入。

除了 @Autowired 注解，Spring 还支持通过 Java 扩展库中的 @Resource 注解来进行依赖注入：

```java
@Component
public class A {
    @Resource
    private B b;
}

@Component
public class B {
}
```

@Resource 注解默认是根据 Bean 的名称进行依赖注入的，我们可以通过它的 name 属性指定 Bean 的名称，如果不指定的话，默认就是根据字段名进行注入，如果根据名称找不到依赖项，则会根据类型找。

除了注入依赖，Spring 还提供了一个 @Value 注解，用来注入外部属性，通常我们会用它来注入某个配置文件中的字段：

```java
@Component
public class A {
    @Value("${app.name:dog}") // 表示注入某个配置文件中的app.name字段，默认值为dog
    private String name;
}
```

上述这种基于注解注册 Bean 的方式需要一个前提，就是要开启 Spring 的组件扫描。Spring 是允许通过 Java 类定义配置信息的，我们可以创建一个 Java 类，加上 @Configuration 注解，并通过 @ComponentScan 注解开启组件扫描：

```java
@Configuration
@ComponentScan
public class AppConfig {
}
```

@ComponentScan 注解默认指示 Spring 去扫描当前配置类所在的包及其子包，也可以通过 value 属性指定具体要扫描的包。这样，在创建 Spring 容器时，就可以通过让 Spring 容器读取这个配置类来获取要注册的 Bean 的信息。

2）基于 Java 类注册 Bean：

Spring 提供了一个 @Configuration 注解用于将某个 Java 类标记为一个配置类，然后在其中可以通过 @Bean 注解实现 Bean 的注册：

```java
@Configuration
public class AppConfig {

    @Bean
    public A a(B b) {
        return new A(b);
    }

    @Bean
    public B b() {
        return new B();
    }
}
```

@Bean 注解表示要将方法的返回值注册为 Bean，我们可以通过 @Bean 注解的 value 属性手动指定 Bean 的名称，如果不指定，默认就是方法名。如果一个 Bean 依赖另一个 Bean，可以直接在方法形参中声明所依赖的 Bean，Spring 会自动完成依赖注入。

这种方式通常是用来注册第三方库中的 Bean，或者某些初始化逻辑比较复杂的 Bean。

### 2.3. Bean 的定制

在注册 Bean 的时候，不仅仅可以给 Bean 起名字，还可以设置 Bean 的作用域、生命周期方法等。

比如，在基于注解注册 Bean 时，还可以通过 @Scope 注解指定 Bean 是单例模式（singleton）还是原型模式（prototype），默认就是单例模式。还可以通过 @PostConstruct 注解和 @PreDestroy 注解指定 Bean 的初始化方法和销毁方法。

```java
@Component
@Scope("prototype")
public class A {
    
    @PostConstruct
    public void init() {
        System.out.println("init...");
    }

    @PreDestroy
    public void destroy() {
        System.out.println("destroy...");
    }
}
```

在基于 Java 类注册 Bean 时，也可以实现类似的定制：

```java
@Configuration
public calss AppConfig {
    
    @Bean(initMethod = "init", destroyMethod = "destroy")
    @Scope("prototype")
    public A a(){
        return new A();
    }
}

public class A {
    public void init() {
        System.out.println("init...");
    }

    public void destroy() {
        System.out.println("destroy...");
    }
}
```
