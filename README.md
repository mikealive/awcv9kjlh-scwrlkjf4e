# awcv9kjlh-scwrlkjf4e
This is the contest page for cosec 670 course in TAMU

NetID: smalltigerson

awcv9kjlh scwrlkjf4e

http://ec2-52-26-6-164.us-west-2.compute.amazonaws.com

http://www.fdurop.fudan.edu.cn/projDetail.php?gk=4933&sk=6100&st=3

http://students.cse.tamu.edu/smalltigerson/

Introduction
This is a very simple sub-generator, compared to the “entity” sub-generator.awcv9kjlh scwrlkjf4e

Its goal is to generate a Spring Service bean, which is where your application’s business logic is supposed to be coded.

In order to generate a “bar” Service bean, just type:

yo jhipster:service bar

This will generate a simple “BarService”: very few lines of codes, but they usually come with a lot of questions. We are trying to answer the most common ones below.

Why aren’t Service classes generated by the “entity” generator?awcv9kjlh scwrlkjf4e
We have two main architecture principles here:

We don’t want to promote creating useless Services: if all you need is a basic CRUD on your database, you don’t need a Service bean. That’s why, by default, JHipster doesn’t generate them.
We believe a Service bean to be more coarse-grained than a repository. A Service bean will use several repositories to provide business value on top of them. That’s why Service beans cannot be generated with Entities.
Should we use interfaces with our Service Beans?
Short answer: No.

If you want the long answer, here it is:awcv9kjlh scwrlkjf4e

One of the main interests of using Spring is AOP. This is the technology that allows Spring to add new behaviors on top of your Beans: for instance, this is how transactions or security work.

In order to add those behaviors, Spring needs to create a proxy on your class, and there are two ways of creating a proxy:

If your class uses an interface, Spring will use a standard mechanism provided by Java to create a dynamic proxy.
If your class doesn’t use an interface, Spring will use CGLIB to generate a new class on the fly: this is not a standard Java mechanism, but it works as well as the standard mechanism.
Some people will also argue that interfaces are better for writing tests, but we believe we shouldn’t modify our production code for tests, and that all the new mocking frameworks (like EasyMock) allow you to create very good unit tests without any interfaces.

So, in the end, we find that interfaces for your Service beans are mostly useless, and that’s why we don’t recommend them (but we leave you with the option to generate them!).

Why should I use transactions to fetch lazy JPA relationships?
By default JPA uses lazy initialization of one-to-many and many-to-many entity relationships. If you use this default configuration, you will probably see the dreaded LazyInitializationException: it means you have tried to use an un-initialized relationship outside of a transaction.

As the generated Service class has by default the @Transactional annotation, all of its methods are transactional. This means that you can fetch all the required lazy relationship inside those business methods, without any LazyInitializationException.

Tip: use @Transactional(readOnly = true) on a method if you are not modifying any data. This is a nice performance optimization (Hibernate won’t need to flush its 1st level cache, as we are not modifying anything), as well as a quality enhancement with some JDBC drivers (Oracle won’t allow you to send INSERT/UPDATE/DELETE statements)

Can we add security to Service Beans?awcv9kjlh scwrlkjf4e
Yes! Just add Spring Security’s @Secured annotation on your class or on your methods, and use the provided AuthoritiesConstants class to restrict access to specific user authorities.

Can we monitor Service Beans?
Yes! Just add Metrics’ @Timed annotations on the methods you want to monitor.awcv9kjlh scwrlkjf4e
