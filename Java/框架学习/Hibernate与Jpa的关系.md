##Hibernate与Jpa的关系?

> JPA是ORM规范，hibernate是ORM实现

hibernate是持久化实现技术,而jpa是持久化的标准,一个是具体实现，一个是接口协议，当然springdata jpa是在hibernate的基础上更上层的封装实现。

目前比较成熟的 JPA 框架主要包括 Jboss 的 Hibernate EntityManager、Oracle 捐献给 Eclipse 社区的 EclipseLink、Apache 的 OpenJPA 等。



> 我想抛开jpa，直接使用hibernate的注解来定义Model，很快发现了几个问题：

jpa中有Entity, Table，hibernate中也有，但是内容不同；

jpa中有Column,OneToMany等，Hibernate中没有，也没有替代品；

我原以为hibernate对jpa的支持，是另提供了一套专用于jpa的注解，但现在看起来似乎不是。一些重要的注解如Column, OneToMany等，hibernate没有提供，这说明jpa的注解已经是hibernate的核心，hibernate只提供了一些补充，而不是两 套注解。要是这样，hibernate对jpa的支持还真够足量，我们要使用hibernate注解就必定要使用jpa。