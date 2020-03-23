Spring AOP

Aspect-Oriented Programming (AOP) complements Object-Oriented Programming (OOP) by providing another way of thinking about program structure. 

The key unit of modularity in OOP is the **class**, whereas in AOP the unit of modularity is the **aspect**.

Aspects enable the modularization of crosscutting concerns such as transaction management, security, logging, auditing, caching or  custom aspects, complementing their use of OOP with AOP.

Spring uses **proxy based mechanism** i.e. it creates a proxy Object which will wrap around the original object and will take up the advice which is relevant to the method call. Proxy objects can be created either manually through proxy factory bean or through auto proxy configuration in the XML file and get destroyed when the execution completes. Proxy objects are used to enrich the Original behaviour of the real object.

```java
//Create the Proxy Factory
AspectJProxyFactory proxyFactory = new AspectJProxyFactory(student);

//Add Aspect class to the factory
proxyFactory.addAspect(Logging.class);

//Get the proxy object
Student proxyStudent = proxyFactory.getProxy();

//Invoke the proxied method.
proxyStudent.getAge();
```

Aspect Oriented Programming..

![](https://raw.githubusercontent.com/praveenambati1233/Spring/master/AOP_concept.PNG?token=AL5BQD7HEBFROJYDPFBJ7MC6PBTYC)

**Steps in AOP**
1. write Aspects
2. configuration where the aspects apply using @Advice on **class** ( spring bean)
3. Enable AOP in applicationContext file  	`<aop:aspectj-autoproxy></aop:aspectj-autoproxy>`


Types of advice:

- Aspect 

A module which has a set of APIs providing cross-cutting requirements. For example, a logging module would be called AOP aspect for logging. An application can have any number of aspects depending on the requirement.  

**Annotation** - @Aspect

- PointCut

This is a set of one or more joinpoints where an advice should be executed. You can specify PointCuts using expressions or patterns as we will see in our AOP examples.
Annotation - @PointCut


```java
    @Pointcut("execution(public * *(..))")
    private void anyPublicOperation() {}
    
    @Pointcut("within(com.xyz.someapp.trading..*)")
    private void inTrading() {}
    
    @Pointcut("anyPublicOperation() && inTrading()")
    private void tradingOperation() {}
```


Advice : action taken by an aspect at a particular join point


Before :  @Before





