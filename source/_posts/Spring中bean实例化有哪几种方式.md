---
title: Spring中bean实例化有哪几种方式(依赖注入)?
date: 2021-01-15 15:37:31
tags: [面试, SSM]
category: [面试, SSM]
---

# Set方法

```java
public class SpringAction {  
    private SpringDao springDao;  
    public void setSpringDao(SpringDao springDao) {  
        this.springDao = springDao;
    }  
    public void doMethod(){  
        springDao.doMethod();  
    }  
}  

<bean name="springAction" class="xxx.SpringAction">  
    <property name="springDao" ref="springDao"></property>
</bean>  
<bean name="springDao" class="xxx.impl.SpringDaoImpl"></bean>  
```

# 普通构造方法

```java
public class SpringAction {  
    private SpringDao springDao;   
    public SpringAction(SpringDao springDao){  
        this.springDao = springDao;  
    }
    public void doMethod(){  
        springDao.doMethod();  
    }  
}  

 <bean name="springAction" class="xxx.SpringAction">  
    <constructor-arg index="0" ref="springDao"></constructor-arg>  
</bean>
<bean name="springDao" class="xxx.impl.SpringDaoImpl"></bean>  
```

# 静态工厂

```java
public class SpringAction {  
    private FactoryDao staticFactoryDao;   
    public void setStaticFactoryDao(FactoryDao staticFactoryDao) {  
        this.staticFactoryDao = staticFactoryDao;  
    }  
}  

public class DaoFactory {  
    public static final FactoryDao getStaticFactoryDaoImpl(){  
        return new StaticFacotryDaoImpl();  
    }  
} 

<bean id="bean2" class="xxx.StaticFactory" factory-method="getInstance"/>
<bean name="springAction" class="xxx.SpringAction" >  
    <property name="staticFactoryDao" ref="staticFactoryDao"></property>
</bean>  
<bean name="staticFactoryDao" class="xxx.DaoFactory" factory-method="getStaticFactoryDaoImpl"></bean>  
```

# 实例工厂

```java
public class SpringAction {  
    private FactoryDao factoryDao;  
    public void setFactoryDao(FactoryDao factoryDao) {  
        this.factoryDao = factoryDao;  
    }  
}  

public class DaoFactory {   
    public FactoryDao getFactoryDaoImpl(){  
        return new FactoryDaoImpl();  
    }  
}  

<bean name="springAction" class="xxx.SpringAction">   
    <property name="factoryDao" ref="factoryDao"></property>  
</bean>  
<bean name="daoFactory" class="xxx.DaoFactory"></bean>  
<bean name="factoryDao" factory-bean="daoFactory" factory-method="getFactoryDaoImpl"></bean>  
```
