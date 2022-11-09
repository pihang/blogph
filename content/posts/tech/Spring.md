---
title: "Spring"
date: 2022-08-29T13:23:47+08:00
lastmod: 2022-08-29T13:23:47+08:00
author: ["Pihang"]
keywords: 
- 
categories: 
- 
tags: 
- 
description: ""
weight:
slug: ""
draft: false # 是否为草稿
comments: true
reward: true # 打赏
mermaid: true #是否开启mermaid
showToc: true # 显示目录
TocOpen: true # 自动展开目录
hidemeta: false # 是否隐藏文章的元信息，如发布日期、作者等
disableShare: true # 底部不显示分享栏
showbreadcrumbs: true #顶部显示路径
cover:
    image: "" #图片路径例如：posts/tech/123/123.png
    caption: "" #图片底部描述
    alt: ""
    relative: false
---

# Spring


### 一、Spring是什么？****Spring的优点有啥？****

Spring是轻量级的开源的javaEE（Java enterprise edition）企业级开发框架

<aside>
💡 Spring是一个一站式的轻量级的java开发框架，核心是控制反转（IOC）和面向切面（AOP），针对于（包括：）开发的Web层（SpringMVC）、业务层（IOC）、持久层（jdbctemplate）等都提供了多种配置

</aside>

优点：

（1）spring属于低侵入式设计，代码的污染极低；

（2）spring的DI机制将对象之间的依赖关系交由框架处理，减低组件的耦合性；

（3）Spring提供了AOP技术，支持将一些通用任务，如安全、事务、日志、权限等进行集中式管理，从而提供更好的复用。

（4）spring对于主流的应用框架提供了集成支持。

<aside>
💡 IOC让相互协作的组件保持松散的耦合，而AOP编程允许你把遍布于应用各层的功能分离出来形成可重用的功能组件。

</aside>

### 二、谈谈对Spring的IOC理解？

（1）什么是IOC

IOC（Inversion of Control）:**控制反转**，指**将对象的控制权转移给Spring**容器[解耦，实现低耦合]，由Spring来负责控制对象的生命周期（如创建、管理、执行、销毁）以及对象间的依赖关系。

通俗来说：以前创建对象的时机和主动权都是由自己把控的，如果在一个对象中使用另外的对象，就必须主动通过new指令去创建依赖对象（会导致高耦合），使用完后还需要销毁（比如Connection等），对象始终会和其他接口或类耦合起来。       而 IOC 则是由专门的容器来帮忙创建对象(`BeanFactory`)，将所有的类都在 Spring 容器中登记（`BeanDefinition`），当需要某个对象时，不再需要自己主动去 new 了，只需告诉 Spring 容器，然后 Spring 就会在系统运行到适当的时机，把你想要的对象主动给你。

也就是说，对于某个具体的对象而言，以前是由自己控制它所引用对象的生命周期，而在IOC中，所有的对象都被 Spring 控制，**控制对象生命周期的不再是引用它的对象，而是Spring容器，由 Spring 容器帮我们创建、查找及注入依赖对象**，而引用对象只是被动的接受依赖对象，所以这叫控制反转（对组件对象的控制从代码本身转移到了外部容器）。

（2）什么是DI

DI（Dependency Injection）：**依赖注入（通常@Autowired注解自动注入）**。在程序**运行时**，**动态的**向某个对象提供它所需要的其他对象，这一点是通过DI来实现的，即应用程序在运行时依赖 IoC 容器来动态注入对象所需要的外部依赖。而 Spring 的 DI 具体就是通过**反射实现注入**的，反射允许程序**在运行的时候动态的生成对象、执行对象的方法、改变对象的属性**。

（3）IOC的原理

Spring 的 IoC 的实现原理就是**工厂模式**加**反射机制**。工厂相对应的就是**beanfactory接口**
的**getBean()**方法，反射就是Spring底层**实例化对象**所采用的机制。

### 三、****BeanFactory 和 ApplicationContext有什么区别？****

![Untitled](Spring%209cadae506e1543bd828625d230e6aa98/Untitled%201.png)

首先都是Spring的两大**核心接口**，都可以当作Spring的**容器**。

1）BeanFactory是Spring里最底层（父类）的接口，定义了IOC的基本功能[**基础容器**]，包含了各种Bean的定义、加载、实例化、依赖注入和生命周期管理。
补充：Bean的“工厂”**主要职责就是生产Bean，**最强大的工厂是：**DefaultListableBeanFactor类。**
Spring底层就是使用的该实现工厂进行生产Bean的。

2）ApplicationContext接口作为BeanFactory的子类，除了提供BeanFactory所具有的功能外，还提供了更完整的功能（如支持国际访问，资源获取，支持多种消息）[**高级容器**]。

• **BeanFactorty**接口提供了配置框架及基本功能，但是**无法支持spring的aop功能和web应用**。而ApplicationContext接口作为BeanFactory的派生，因而提供BeanFactory所有的功能。（**BeanFactory**
是Spring的**心脏**，那么**ApplicationContext**就是**完整的躯体**了）

### 追问、****BeanFactory 和FactoryBean有什么区别？****

上面的BeanFactory与Applicationcontext更有可比性，他们都可以作为容器，且ApplicationContext实现了BeanFactory的接口。但是**BeanFactory**与**FactoryBean**两者除了名字像一点以外没有什么可比性！

1）**BeanFactory**是一个工厂（最基本的接口），也就是一个**容器**，是来**管理和生产bean**的；

2）**FactoryBean**是一个bean，**但是它是一个特殊的bean（非容器）**，所以也是**由BeanFactory来管理**的， 它是一个**接口**，他必须**被一个bean去实现**。  

补充：如果bean A**实现了FactoryBean接口，那么A就变成了工厂，getObject()返回的对象是工厂产生的对象，而不是A本身**。

### 四、谈谈Spring的AOP理解？

AOP（Aspect Oriented Programming）：**面向切面**。

1）OOP面向对象，允许开发者定义纵向的关系，但并不适用于定义横向的关系（会导致大量代码的重复，而不利于各个模块的重用）。   所以AOP提供一种**横切关注点**（面向切面）的机制，用于将那些与业务无关，但却对多个对象产生影响的公共行为和逻辑【如权限认证、日志、事务处理】，抽取并封装为一个可重用的模块，这个模块被命名为**“切面”（Aspect）。**好处是减少系统中的重复代码，降低了模块间的耦合度，提高系统的可维护性。

2）AOP实现的关键在于 **代理模式**，AOP代理主要分为静态代理和动态代理。静态代理的代表为AspectJ；动态代理则以Spring AOP为代表。

- AspectJ是静态代理，也称为**编译时增强**。在编译阶段生成AOP代理类，并将AspectJ(切面)织入到Java字节码中，运行的时候就是增强之后的AOP对象。（编译阶段插入切面）
- Spring AOP使用的动态代理，动态代理就是说**AOP框架不会去修改字节码**，而是每次**运行时**在内存中临时为方法生成一个AOP对象，这个AOP对象**通过反射**包含了目标对象的全部方法，并且在特定的切点做了增强处理，并回调原对象的方法。（运行时反射临时加入aop增强切面调原方法）

<aside>
💡 静态代理与动态代理区别在于**生成AOP代理对象的时机不同**，相对来说AspectJ的静态代理方式具有更好的性能，但是AspectJ需要特定的编译器进行处理，而Spring AOP则无需特定的编译器处理。

</aside>

### 追问：讲一下Spring AOP里面的几个名词？

![**目标对象**（Target）：需要被织入关注点的对象。即被代理的对象。
**代理**（Proxy）：通过代理方式来对目标对象应用切面。AOP代理可以用JDK动态代理或CGLIB代理
实现。
**通知**（Advice）：在连接点上执行的行为，增强提供了在AOP中需要在切入点所选择的连接点处进
行扩展现有行为的手段。包括**前置增强（before advice）、后置增强 (after advice)、环绕增强
（around advice）**。](Spring%209cadae506e1543bd828625d230e6aa98/Untitled%202.png)

**目标对象**（Target）：需要被织入关注点的对象。即被代理的对象。
**代理**（Proxy）：通过代理方式来对目标对象应用切面。AOP代理可以用JDK动态代理或CGLIB代理
实现。
**通知**（Advice）：在连接点上执行的行为，增强提供了在AOP中需要在切入点所选择的连接点处进
行扩展现有行为的手段。包括**前置增强（before advice）、后置增强 (after advice)、环绕增强
（around advice）**。

### 五、探讨AOP的两种动态代理？

Spring AOP中的动态代理主要有两种方式，JDK动态代理和CGLIB动态代理：
1）JDK动态代理只提供接口及接口实现类的代理，**不支持类的代理**。JDK动态代理的核心是**InvocationHandler接口**和**Proxy类**。使用Proxy类动态创建目标类的代理对象；然后代理对象通过InvocationHandler接口的invoke()方法反射来调用目标类中的代码，动态地将横切逻辑和业务编织在一起（代码增强）。

<aside>
💡 InvocationHandler接口 的 **invoke**(Object proxy,Method method,Object[] args)方法：
proxy是最终生成的代理对象；  method是被重写的方法；

</aside>

2）CGLIB（Code Generation Library）动态代理：如果被代理类**没有实现接口**，就用CGLIB来动态代理目标类。CGLIB是**通过继承**的方式动态的生成指定类的一个子类对象，并**覆盖其中特定方法并添加增强代码**，从而实现AOP。（因此如果某个类被标记为final，那么它是无法使用CGLIB）

### 六、****Spring Bean的生命周期？****

简单来说，Spring Bean的生命周期只有四个阶段：

**实例化** Instantiation (与BeanPostProcessor的**子接口**`InstantiationAwareBeanPostProcessor`有关)-->

**属性赋值** Populate ( 属性设置与依赖注入)--> 

**初始化** Initialization （`BeanPostProcessor`接口前置后置处理，这步后bean被创建）--> 

**销毁** Destruction （调用destroy()方法或配置destroy-method属性）

ps:前两个阶段对应构造方法和setter方法的注入，后两个阶段可以由用户自定义

![Untitled](Spring%209cadae506e1543bd828625d230e6aa98/Untitled%203.png)

1）**实例化Bean: 对于`BeanFactory`(组件工厂)容器调用createBean进行实例化**；对于ApplicationContext容器，当容器启动结束后，通过获取BeanDefinition对象中的信息，实例化所有的bean。

2）**设置对象属性（依赖注入**）：实例化后的对象被封装在`BeanWrapper对象`中，容器根据`BeanDefinition`中的信息 以及 通过BeanWrapper提供的设置属性的接口完成属性设置与依赖注入。

**Spring会检测该对象是否实现了xxxAware接口，通过Aware类型的接口，对应名称调用方法资源**

3）**BeanPostProcessor前置处理**：对Bean进行一些自定义的前置处理，那么可以让Bean组件实现了`BeanPostProcessor`接口；  在**调用初始化方法**，可以Bean实现了InitializingBean接口，首先属性设置方法；还有个组件配置了init-method 属性，则会自动调用其配置的初始化方法。

**BeanPostProcessor后置处理**：由于这个方法是在Bean初始化结束时调用的，所以可以被应用于内存或缓存技术。

> 以上几个步骤完成后，Bean就已经被正确创建了，之后就可以使用这个Bean了。
> 

4)**销毁Bean**: destroy()方法或者Bean的Spring配置中配置了destroy-method属性，会自动调用其配置的销毁方法。

### 七、****Spring中bean的作用域？****

（1）**singleton**：默认作用域，**单例bean，每个容器中只有一个bean的实例**。

（2）**prototype**：为每一个bean请求创建一个实例。

（3）**request**：为每一个request请求创建一个实例，在请求完成以后，bean会失效并被垃圾回收器回收。

（4）**session**：与request范围类似，同一个session会话共享一个实例，不同会话使用不同的实例。

（5）**global-session**（不常用）：全局作用域，所有会话共享一个实例。如果想要声明让所有会话共享的存储变量的话，那么这全局变量需要存储在global-session中。

### 八、spring容器的启动流程分哪些？

1）初始化Spring容器，注册内置的BeanPostProcessor的`BeanDefinition`到容器中：

- 实例化BeanFactory【DefaultListableBeanFactory】工厂，用于生成Bean对象
- 实例化BeanDefinitionReader注解配置读取器，用于对特定注解（如@Service、@Repository）的类进行读取转化成 BeanDefinition 对象

<aside>
💡 BeanDefinition 存储了 bean 对象的所有特征信息，如是否单例，是否懒加载，factoryBeanName 等

</aside>

- 实例化ClassPathBeanDefinitionScanner路径扫描器，用于对指定的包目录进行扫描查找 bean 对象

2）将配置类的BeanDefinition注册到容器中

3）调用refresh()方法刷新容器：有些bean的生命周期内容

### 九、****Spring如何解决循环依赖？****

[(48条消息) Spring如何解决循环依赖_意田天的博客-CSDN博客_spring如何解决循环依赖](https://blog.csdn.net/A_Java_Dog/article/details/117192587?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166056851716780357238701%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=166056851716780357238701&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_click~default-2-117192587-null-null.142^v40^new_blog_pos_by_title,185^v2^control&utm_term=Spring%E5%A6%82%E4%BD%95%E8%A7%A3%E5%86%B3%E5%BE%AA%E7%8E%AF%E4%BE%9D%E8%B5%96&spm=1018.2226.3001.4187)

一个对象一般创建过程有3部分组成：

1. 实例化：简单理解就是new了一个对象
2. 属性注入：为实例化中new出来的对象填充属性
3. **初始化：执行aware接口中的方法，初始化方法，完成AOP代理**

解决循环依赖实际就是三级缓存，可以理解为3个Map:

1、singletonObjects：一级，日常实际获取Bean的地方

2、earlySingletonObjects：二级，已实例化，但还没进行属性注入，由三级缓存放进来

3、singletonFactories：三级，value是一个**对象工厂（可以从里面拿到代理对象）**

> 对象Object和`对象工厂ObjectFactory`是不一样的！！！
> 

答：

当A、B两个类发生循环引用时，在A完成实例化后，就使用实例化后的对象去创建一个`对象工厂`，添加到三级缓存中，**如果A被AOP代理，那么通过这个工厂获取到的就是A`代理后`的对象**，如果A没有被AOP代理，那么这个工厂获取到的就是A实例化的对象。

当A进行属性注入时，会去创建B，同时B又依赖了A，所以创建B的同时又会去调用getBean(a)来获取需要的依赖，此时的getBean(a)会从缓存中获取：

<aside>
💡 `对象工厂`：A**实现了FactoryBean接口，那么A就变成了工厂，getObject()返回的对象是工厂产生的对象（非A对象），放入三级缓存**

</aside>

![Untitled](Spring%209cadae506e1543bd828625d230e6aa98/Untitled%204.png)

![三级缓存](Spring%209cadae506e1543bd828625d230e6aa98/Untitled%205.png)

三级缓存

问追、为什么需要三级缓存？

首先，实际上两级缓存就能解决循环依赖，但不满足Spring AOP的特性不可取。

比如：我们对象是单例的，有可能A对象依赖的B对象是有AOP的（那么B对象需要代理）。**假设没有第三级缓存，只有第二级缓存（value存对象，而不是工厂对象）**。那如果有AOP的情况下，岂不是在存入第二级缓存之前都要先去做AOP代理？这不合适。【**Spring设计原则：最后一步完成代理**而不是在实例化后就立马完成AOP代理】

反例只用二级缓存：

A调B，A是AOP增强的对象; B循环依赖A,so B依赖得到的A一定是代理对象（需要是事先完成AOP代理），这样违反了Spring设计原则（**不是所有Bean在实例化后就要完成AOP代理，应该有些在Bean初始化最后阶段**）

![二级缓存](Spring%209cadae506e1543bd828625d230e6aa98/Untitled%206.png)

二级缓存

### 十、****Spring框架中的Bean是线程安全的么？如果线程不安全，那么如何处理？****

Spring容器本身并没有提供Bean的线程安全策略，因此可以说Spring容器中的**Bean本身不具备线程安全**的特性，但是具体情况还是要结合Bean的作用域来讨论。

（1）对于prototype作用域的Bean，每次都创建一个新对象，也就是线程之间不存在Bean共享，因此不会有线程安全问题。

（2）对于singleton作用域的Bean，所有的线程都共享一个单例实例的Bean，因此是存在线程安全问题的。但是如果单例Bean是一个无状态Bean，也就是线程中的操作不会对Bean的成员执行查询以外的操作，那么这个单例Bean是线程安全的。比如Controller类、Service类和Dao等，这些Bean大多是无状态的，只关注于方法本身。
解决方法：

最浅显的解决办法就是将有状态的bean的**作用域由“singleton”改为“prototype”**。

也可以采用ThreadLocal解决线程安全问题，为每个线程提供一个独立的变量副本，不同线程只操作自己线程的副本变量。

### 十一、讲一讲****Spring事务？****

**Spring事务的本质其实就是数据库对事务的支持**，没有数据库的事务支持，spring是无法提供事务功能的。Spring只提供统一事务管理接口，具体实现都是由各数据库自己实现，数据库事务的提交和回滚是通过 redo log 和 undo log实现的。Spring会在事务开始时，根据当前环境中设置的隔离级别，调整数据库隔离级别，由此保持一致。
**Spring事务的种类：编程式事务管理**和**声明式事务管理**

编程式事务管理使用TransactionTemplate。

声明式事务管理建立在AOP之上的。其本质是通过AOP功能，对方法前后进行拦截，将事务处理的功能编织到拦截的方法中，也就是在目标方法开始之前启动一个事务，在执行完目标方法之后根据执行情况提交或者回滚事务。

<aside>
💡 声明式事务最大的优点就是不需要在业务逻辑代码中掺杂事务管理的代码，只需在配置文件中做相关的事务规则声明或通过@Transactional注解的方式，便可以将事务规则应用到业务逻辑中，减少业务代码的污染。唯一不足地方是，最细粒度只能作用到方法级别，无法做到像编程式事务那样可以作用到代码块级别。

</aside>