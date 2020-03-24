Spring AOP

Aspect-Oriented Programming (AOP) complements Object-Oriented Programming (OOP) by providing another way of thinking about program structure. 

The key unit of modularity in OOP is the **class**, whereas in AOP the unit of modularity is the **aspect**.

Aspects enable the modularization of crosscutting concerns such as transaction management, security, logging, auditing, caching or  custom aspects, complementing their use of OOP with AOP.

Cross cutting corners :

Cross cutting concerns are 'things' you want to do in multiple places in your application.

- Logging REST call
- Gathering metrics on method calls
- Only let 'admin' users access functionality
- Only let requests from localhost access functionality

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

Annotation - @Aspect

- PointCut

Since it is not feasible to apply advice at every point of the code, therefore, the selected join points where advice is finally applied are known as the Pointcut. Often you specify these pointcuts using explicit class and method names or through regular expressions that define a matching class and method name patterns. It helps in reduction of repeating code by writing once and use at multiple points, let’s see how.

Annotation - @PointCut


```java
    @Pointcut("execution(public * *(..))")
    private void anyPublicOperation() {}
    
    @Pointcut("within(com.xyz.someapp.trading..*)")
    private void inTrading() {}
    
    @Pointcut("anyPublicOperation() && inTrading()")
    private void tradingOperation() {}
```

Target object

The object being advised by one or more aspects. This object will always be a proxied object. Also referred to as the advised object.

- Weaving

Weaving is the process of linking aspects with other application types or objects to create an advised object. This can be done at compile time, load time, or at runtime.

- Advice

This is the actual action to be taken either before or after the method execution. This is the actual piece of code that is invoked during program execution by Spring AOP framework.

**Type of Advices**

- Before

@Before is an advice type which ensures that an advice runs before the method execution. Following is the syntax of @Before advice.

- After

@After is an advice type which ensures that an advice runs after the method execution. Following is the syntax of @After advice.

- after-returning 

Runs after the advised method successfully completes ie without any runtime exceptions.

How to  capture return value of the method that being called ?
```java
@AfterReturning(returning="returnObject")
public void returnObject(Object returnObject){
s.o.p("reutrn value"+returnObject)
}
```

- AfterThrowing

Runs after the advised method throws a Runtime Exception. It is denoted by @AfterThrowing annotation.

- around

This is the strongest advice among all the advice since it wraps around and runs before and after the advised method. This type of advice is used where we need frequent access to a method or database like- caching. It is denoted by @Around annotation.

Around object(ProceedingJoinPoint.process) has controll to change the "after returning" value and send back to adviced/caller. 

```java
public Object  logAroundAllMethods(ProceedingJoinPoint proceedingJoinPoint) throws Throwable 
{
    Object returnValue = null;
	try{
	System.out.println("****LoggingAspect.logAroundAllMethods() - Before method call");
     
    returnValue = proceedingJoinPoint.proceed();
     
    System.out.println("****LoggingAspect.logAroundAllMethods() - After method call");
	}catch(Exception e){
	System.out.println("******After throwing exception*****");
	}
	
	System.out.println("******After throwing exception*****");
	return returnValue;
}

```

 Custom annotation which can be market as an Advice on given  method : 
 
 1. create annotation.
 2. provide annotation in the pointcut expression

when you want to run Advice on particular method  you can Annotate like below,

Step 1 :

```java
package room.aop.aspects;
public @interface Loggable {
}
```
Step 2

```java
@Around("@annotation(room.aop.aspects.Loggable)")
	public void logAllMethod(ProceedingJoinPoint joinPoint) throws Throwable{
	
		System.out.println("Before advice");
		joinPoint.proceed();
		System.out.println("After advice");
	}
```

```java
@Loggable
	public String getName() {
		System.out.println(name);
		return name;
	}
```
	
```java
ApplicationContext applicationContext = new ClassPathXmlApplicationContext("spring-context.xml");
				ShapeService service =  applicationContext.getBean("shapeService",ShapeService.class);
		service.getTraingle().getName();
```
output :
```java
Before advice
After advice
```


**Important methods  : **

**JoinPoint **-  contains all the information of the method called. 

joinPoint.getTarget() -- provides all





TODO -  https://stackoverflow.com/questions/60816175/how-to-ignore-aop-exceptions-and-continue-with-service-logic
