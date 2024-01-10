### [Spring学习笔记](https://plusw.github.io/blog/#article/article03learnSpringBoot)
*2024,01.09*  
    最近想转行java,发现找工作很多是要熟悉spring boot，于是开启了我的Spring学习之路, 这里是我的学习笔记，方便日后查阅。

##### **前言**
*全栈之路，出发!!*
如果你是初学者，可以先学习Spring Boot，因为它更容易上手，可以让你快速搭建起一个简单的Spring应用。
一旦你对Spring Boot有了一定的了解，再深入学习Spring框架，掌握更多的高级特性和概念。
##### **了解Spring Boot的基本概念**  
1.默认配置被广泛使用，你只需要在需要特殊配置的情况下进行配置。Spring Boot通过自动配置机制，减少了手动配置的需要。  
2.Spring Starter 是 Spring 框架提供的一种用于简化项目配置和快速启动的工具，Spring Starter 提供了一种简单的方式来添加依赖项、配置和默认设置。
3.Spring Boot应用程序的入口类通常包含main方法，并使用一些注解。
``` java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class MyApplication {
    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}
```
 