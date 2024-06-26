theme: OCI White
slidenumbers: false
[.hide-footer]

![original](images/oci-backgrounds/oci-intro.png)

```
```
```
```
```
```
# [FIT] **GRAILS 4 STATUS UPDATE**
> _Bringing Micronaut Goodness to Grails_

```
```

---

![original](images/oci-backgrounds/oci-white.png)

# About Me

* Graeme Rocher
* Creator of Grails and Micronaut
* Principal Engineer at Object Computing
* Oracle Groundbreaker Award Winner

---

![original](images/oci-backgrounds/oci-white.png)

# Agenda

* Introduction to Micronaut 
* Introduction to Grails 4
* Grails vs Micronaut
* Using Micronaut Features in Grails
* Demos

----

![original](images/oci-backgrounds/oci-white.png)

# Micronaut for Grails Developers

* Micronaut a Foundational Library for building applications of any type
* Focuses on Small Memory Footprint and Speed
* Eliminates Reflection, Runtime Proxies and Runtime Analysis

![right, 35%](images/micronaut-stack-blue.png)

----

![original](images/oci-backgrounds/oci-white.png)

# Why Micronaut?

* Micronaut uses no reflection, no runtime proxies, no runtime byte code generation etc.
* Eliminating these leads to reduced memory consumption and faster startup
* Increasingly important for Microservices, Serverless, IoT, any low-memory footprint environment

![right, 35%](images/micronaut-stack-blue.png)

----
![original](images/oci-backgrounds/oci-white.png)

# Micronaut vs Grails

| Micronaut | Grails |
| --- | --- | 
| Range of Runtimes | Servlet Only | 
| General Purpose | Traditional Servlet Web Apps | 
| DI, AOP etc. | Spring for DI, AOP etc. |
| Java, Kotlin, Groovy, GraalVM | Groovy Only |
| Client and Server | Server Only |

----

![original](images/oci-backgrounds/oci-white.png)

# What's New in Grails 4?

* Dependency Upgrades Galore: Java 8+, Spring 5.1+, Spring Boot 2.1+, Groovy 2.5+, Hibernate 5.4+, Gradle 5+
* Legacy Cleanup
* Faster Startup / Reduced Memory Consumption
* Micronaut Integration

![right, 100%](images/grails.png)

----

![original](images/oci-backgrounds/oci-white.png)

# Grails 4 Current Status

* Grails 4 Milestone 2 Released on Tuesday
* Will soon start RCs
* Plugin testing and Guide migration underway
* Ideally GA in a month or so
* Time to start reporting feedback

![right, 100%](images/grails.png)


----

![original](images/oci-backgrounds/oci-white.png)

# Grails 4 and Micronaut

* Micronaut the Parent `ApplicationContext`
* Made possible by 
	* http://github.com/micronaut-projects/micronaut-spring
* Micronaut Libraries become usable in Grails
* Anything we build for Micronaut benefits Grails	

![right, 100%](images/grails.png)

----

![original](images/oci-backgrounds/oci-white.png)
# What Can/Should You Do 

* Build Configurations (Instead of Plugins)
* Use Declarative Clients
	- HTTP
	- Kafka
	- RabbitMQ
	- More Coming...


![right, 35%](images/micronaut-stack-blue.png)

----
![original](images/oci-backgrounds/oci-white.png)

# Configurations vs Plugins

* Consider Building Configurations instead of Plugins
* Work with Micronaut, Spring (with `micronaut-spring`) and Grails
* Plugins only work with Grails
* ... although some things only possible with Plugins (Views, taglibs etc.)

![right, 35%](images/micronaut-stack-blue.png)

----
![original](images/oci-backgrounds/oci-white.png)
# Micronaut Configurations

* Configuration with `@ConfigurationProperties`
* Beans with `@Singleton`, `@Factory` etc.
* Conditional Behaviour with `@Requires`
* Customization with `@Replaces` 


![right, 35%](images/micronaut-stack-blue.png)

----

![original](images/oci-backgrounds/oci-white.png)

# `@ConfigurationProperties`
### Type Safe Configuration

```java
@ConfigurationProperties("example")
class ExampleConfiguration {
	String name
}


ApplicationContext context = ApplicationContext.run("example.name":"Demo")
FooConfiguration config = context.getBean(FooConfiguration)
assert config.name == 'Demo'
```

----

![original](images/oci-backgrounds/oci-white.png)

# `@Requires`
### Conditional Beans Made Easy

```groovy
@Requires(property="example.enabled")
@Requires(beans=DataSource)
@Requires(missingBeans=Example)
@Singleton
class DefaultExampleBean implements Example {
	...
}

def context = ApplicationContext.run("example.enabled":"true")
Example example = context.getBean(Example)
```

----

![original](images/oci-backgrounds/oci-white.png)

# `@Replaces`
### Easily Replace Beans by Type

```groovy
@Replaces(DefaultExample)
@Singleton
class AlternativeExample implements Example {
	...
}

```

* Types match much
* Beans annotated with `@Infrastructure` not replaceable

----

![original](images/oci-backgrounds/oci-white.png)

# `@Client`
### Declarative Compile Time HTTP Clients

```groovy
@Client("https://api.github.com")
@Header(name="User-Agent", value="micronaut-client")
interface GithubClient {
	@Get("/repos/{+slug}")
	Info getInfo(String slug)
}

```

* Blocking or Non-Blocking (RxJava, Reactor or Future)
* Reflection / Runtime Proxy Free 

----

![original](images/oci-backgrounds/oci-white.png)

# `@Client`


```groovy
compile "io.micronaut:micronaut-http-client"
```

* Uses Micronaut's low-level HTTP client (`RxHttpClient`) under the hood
* Built with Micronaut AOP (reflection/runtime proxy free)
* Works on GraalVM `nativeimage`
* Integrates with Tracing, Metrics, Service Discovery etc.

![right, 35%](images/micronaut-stack-blue.png)

----

![original](images/oci-backgrounds/oci-white.png)

# `@KafkaClient`
### Declarative Compile Time Kafka Clients

```groovy
@KafkaClient 
public interface ProductClient {
    @Topic("my-products") 
    void sendProduct(@KafkaKey String brand, String name); 
}

```

* Blocking or Non-Blocking (RxJava, Reactor or Future)

> https://github.com/micronaut-projects/micronaut-kafka

----

![original](images/oci-backgrounds/oci-white.png)

# `@RabbitClient`
### Declarative Compile Time Rabbit Clients

```groovy
@RabbitClient("animals") 
interface AnimalClient {
    void send(@Header String animalType, Animal animal) 
}

```

* Blocking or Non-Blocking (RxJava, Reactor or Future)

> https://github.com/micronaut-projects/micronaut-rabbitmq

----

![original](images/oci-backgrounds/oci-demo-dark.png)

# [FIT] **DEMO**
## **Micronaut and Grails**

----

![original](images/oci-backgrounds/oci-white.png)

# Micronaut Message Consumers

![original](images/oci-backgrounds/oci-white.png)

* Micronaut Supports Message-Drive Microservices
* Can be run as standalone processes (No HTTP server)
* Use `@RabbitListener` for Rabbit
* Use `@KafkaListener` for Kafka

> https://docs.micronaut.io/1.1.x/guide/index.html#messaging

![right, 35%](images/micronaut-stack-blue.png)


----

![original](images/oci-backgrounds/oci-white.png)

# Micronaut's Clients

![original](images/oci-backgrounds/oci-white.png)

* Compile Time 
* Reflection and Runtime Proxy Free
* Java, Groovy or Kotlin
* Built with Micronaut AOP

> https://docs.micronaut.io/1.1.x/guide/index.html#aop

![right, 35%](images/micronaut-stack-blue.png)

----

# Summary

* Micronaut Provides an Awesome Foundation
* Building Blocks to Create Libraries, Configurations and Clients
* Most Micronaut Features Available in Grails
* Build Micronaut Libraries not Plugins

----

![original](images/oci-backgrounds/oci-demo-dark.png)

# [FIT] **Q & A**

----

![original](images/oci-backgrounds/oci-connect.png)

----

![original](images/oci-backgrounds/oci-training.png)
