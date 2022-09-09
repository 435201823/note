# Spring面试题

## 什么是spring?

Spring是一个开放源代码的设计层面框架，它解决的是业务逻辑层和其他各层的松耦合问题，因此它将面向接口的编程思想贯穿整个系统应用。

通过IOC和AOP的设计达到松耦合的目的。

## Spring由哪些模块组成?

- Spring Context:提供架构式的Bean访问方式
- Spring Core：核心类库，所有功能都依赖于类库，提供了IOC和DI
- Spring Aop： 提供AOP功能
- Spring web：提供了针对Web的综合特性，提供了针对常见框架的支持，能够将对象注入到框架。
- Spring MVC：提供面向Web应用的Model-View-Controller模型框架，即MVC实现。
- Spring DAO: 对JDBC的抽象封装，统一异构的JDBC抽象。
- Spring ORM：对现有ORM框架的支持

## 使用Spring框架的好处是什么?

- 轻量
- 控制反转：通过控制反转实现松耦合，对象们给出他们的依赖，而不是创建或查找依赖的对象们。
- 面向切面编程
- 容器：Spring通过容器管理对象生命周期和配置
- MVC框架
- 事务管理
- 异常处理

## 什么是IOC

IOC，控制反转。获得依赖对象的过程被反转了。控制反转后，通过IOC容器主动将依赖对象注入到对象中。

## 什么是Spring IOC容器

spring IOC将对象存储在容器中，管理对象的生命周期和配置。

## IOC的优点

它将最小化应用程序中的代码量。
它将使您的应用程序易于测试，因为它不需要单元测试用例中的任何单例
或 JNDI 查找机制。
它以最小的影响和最少的侵入机制促进松耦合。
它支持即时的实例化和延迟加载服务。

## 什么是Spring的依赖注入？

不用创建对象，而只需要描述它如何被创建。你不在代码里直接组装你的组件和服务，但是要描述哪些组件需要哪些服务，之后一个容器（IOC容器）负责把它们组装起来。

## 有哪些不同类型的IOC（依赖注入）方式？

**构造器依赖注入**：构造器依赖注入通过容器触发一个类的构造器来实现的，该类有一系列参数，每个参数代表一个对其他类的依赖。
**Setter方法注入**：Setter方法注入是容器通过调用无参构造器或无参static工厂 方法实例化bean之后，调用该bean的setter方法，即实现了基于setter的依赖注入。
**属性注入**： 通过autowire或resource注入

## 哪种依赖注入方式你建议使用，构造器注入，还是 Setter方法注入？

你两种依赖方式都可以使用，构造器注入和Setter方法注入。最好的解决方案是用构造器参数实现强制依赖，setter方法实现可选依赖。

## 为什么不推荐属性注入

- 基于属性注入的方式, 违背单一职责原则
- 基于属性注入的方式, 容易导致Spring 初始化失败（空指针异常）
- 通过@Autowired 注入, 又因为是 ByType 注入, 因此有可能会出现两个相同的类型bean

## 什么是Bean

bean是一个由Spring IoC容器实例化、组装和管理的对象。

## 一个 Spring Bean 定义 包含什么？

一个Spring Bean 的定义包含容器必知的所有配置元数据，包括如何创建一个bean，它的生命周期详情及它的依赖。

## 如何给Spring提供配置元数据

- XML配置文件
- 基于注解进行配置（@Controller，@Service，@Repository，@Component 等）
- 基于java代码进行配置（@Bean）

## 怎么样定义类的作用域

当定义一个\<bean> 在Spring里，我们还能给这个bean声明一个作用域。它可以通过bean 定义中的scope属性来定义。

## Spring支持的集中Bean的作用域

Spring框架支持以下五种bean的作用域：

- singleton：bean在每个Spring ioc 容器中只有一个实例。
- prototype：一个bean的定义可以有多个实例。
- request：每次http请求都会创建一个bean，该作用域仅在基于web的Spring ApplicationContext情形下有效。
- session：在一个HTTP Session中，一个bean定义对应一个实例。该作用域仅在基于web的Spring ApplicationContext情形下有效。
- global-session：在一个全局的HTTP Session中，一个bean定义对应一个实例。该作用域仅在基于web的Spring ApplicationContext情形下有效。

缺省的Spring bean 的作用域是Singleton。

## Spring框架中的单例bean是线程安全的吗？

不，Spring框架中的单例bean不是线程安全的，框架并没有对bean进行多线程的封装处理。那就需要开发人员自己来进行线程安全的保证。

## 解释Spring框架中bean的生命周期

Spring bean的生命周期大致可以分为5个阶段：

- 创建前准备
- 创建实例
- 依赖注入
- 容器缓存
- 销毁实例

创建前准备: 主要作用是Bean在开始加载之前从上下文和配置中解析并查找Bean有关的扩展。比如init-method、destory-method或一些Bean加载的前置后置处理扩展。这些是Spring提供给开发者用于扩展Bean的加载。

创建实例：通过反射创建实例，并扫描Bean的属性

依赖注入： 如果需要实例化的Bean还依赖其他Bean对象，那么就回将依赖的Bean进行对象注入。另外还会调用一些前后置的扩展。

容器缓存阶段： 把Bean保存到容器中，这个阶段的Bean已经可以被开发者使用了。另外还会调用一些前后置的扩展。

销毁实例： Spring的上下文被销毁的时候，上下文中的Bean也会被销毁。如果有配置destory-method，则会被调用。

## 什么是Spring的内部bean？

当一个bean仅被用作另一个bean的属性时，它能被声明为一个内部bean，为了定义inner bean，在Spring 的 基于XML的 配置元数据中，可以在 \<property/>或 \<constructor-arg/> 元素内使用\<bean/> 元素，内部bean通常是匿名的，它们的Scope一般是prototype。

## 在 Spring中如何注入一个java集合？

Spring提供以下几种集合的配置元素：

- \<list>类型用于注入一列值，允许有相同的值。
- \<set> 类型用于注入一组值，不允许有相同的值。
- \<map> 类型用于注入一组键值对，键和值都可以为任意类型。
- \<props>类型用于注入一组键值对，键和值都只能为String类型。

## 什么是bean装配？

在Spring 容器中把bean组装到一起，前提是容器需要知道bean的依赖关系，如何通过依赖注入来把它们装配到一起。

## 什么是bean的自动装配？

Spring 容器能够自动装配相互合作的bean，这意味着容器不需要\<constructor-arg>和\<property>配置，能通过Bean工厂自动处理bean之间的协作。

## 解释不同方式的自动装配

有五种自动装配的方式，可以用来指导Spring容器用自动装配方式来进行依赖注入

- no :默认的方式是不进行自动装配，通过显式设置ref 属性来进行装配。
- ByName：通过参数名 自动装配，Spring容器在配置文件中发现bean的autowire属性被设置成byname，之后容器试图匹配、装配和该bean的属性具有相同名字的bean。
- ByType：通过参数类型自动装配，Spring容器在配置文件中发现bean的autowire属性被设置成byType，之后容器试图匹配、装配和该bean的属性具有相同类型的bean。如果有多个bean符合条件，则抛出错误。
- constructor：这个方式类似于byType， 但是要提供给构造器参数，如果没有确定的带参数的构造器参数类型，将会抛出异常。
- autodetect：首先尝试使用constructor来自动装配，如果无法工作，则使用byType方式。

## 自动装配有哪些局限性？

- 重写：你仍需用 <constructor-arg>和 <property> 配置来定义依赖，意味着总要重写自动装配。
- 基本数据类型：你不能自动装配简单的属性，如基本数据类型，String字符串.
- 模糊特性: 自动装配不如显式装配精确，如果有可能，建议使用显式装配。

## 你可以在Spring中注入一个null 和一个空字符串吗？

可以。

## 什么是基于注解的容器配置？

开发者通过在相应的类，方法或属性上使用注解的方式，直接组件类中进行配置，而不是使用xml表述bean的装配关系。

## 怎样开启注解装配？

注解装配在默认情况下是不开启的，为了使用注解装配，我们必须在Spring配置文件中配置 <
context:annotation-config/>元素。

现在一般是pom中加入注解依赖。

## @Required 注解

这个注解表明bean的属性必须在配置的时候设置，通过一个bean定义的显式的属性值或通过自动装配，若@Required注解的bean属性未被设置，容器将抛出
BeanInitializationException。

## @Resource

## @Autowired

## @Qualifier 注解

## 