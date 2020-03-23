Spring AOP

Aspect-Oriented Programming (AOP) complements Object-Oriented Programming (OOP) by providing another way of thinking about program structure. 

The key unit of modularity in OOP is the **class**, whereas in AOP the unit of modularity is the **aspect**.

Aspects enable the modularization of crosscutting concerns such as transaction management, security, logging, or  custom aspects, complementing their use of OOP with AOP.

Aspect Oriented Programming..

C:\share\desktop\java\webservices\AOP_concept.PNG

AOP concepts :

C:\share\desktop\java\webservices\AOP.PNG

**Steps in AOP**
1. write Aspects
2. configuration where the aspects apply using @Advice on **class** ( spring bean)
3. Enable AOP in applicationContext file  	`<aop:aspectj-autoproxy></aop:aspectj-autoproxy>`


Types of advice:

Advice : 
Before :



wildcards: 




