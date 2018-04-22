---
layout: post
title: Swagger UI
categories: Spring
description: Springfox Swagger UI
keywords: Spring, Springfox, swagger
---

>  THE WORLD'S MOST POPULAR API TOOLING

Spring 整合 swagger-ui

#### 引入依赖

```xml
<!-- springfox是从swagger-springmvc发展而来形成了一个新的组件，
 	 springfox-swagger2是帮助我们自动生成json文件，
 	 springfox-swagger-ui是帮助将json解析出来进行展示-->
<!-- https://mvnrepository.com/artifact/io.springfox/springfox-swagger2 -->
<dependency>
	<groupId>io.springfox</groupId>
	<artifactId>springfox-swagger2</artifactId>
	<version>${swagger2.version}</version>
</dependency>
<!-- https://mvnrepository.com/artifact/io.springfox/springfox-swagger-ui -->
<dependency>
	<groupId>io.springfox</groupId>
	<artifactId>springfox-swagger-ui</artifactId>
	<version>${swagger-ui.version}</version>
</dependency>
```

springfox 是从 swagger-springmvc 发展过来的，以后使用 springfox-swagger2 就可以了，springfox-swagger-ui 是一套前端解析插件

*相关：* [https://github.com/springfox/springfox/blob/master/docs/transitioning-to-v2.md](https://github.com/springfox/springfox/blob/master/docs/transitioning-to-v2.md  )   

#### 资源路径配置

- Spring Boot 不用配置相关资源路径

- 普通 Spring 工程配置如下：

  - 方式一

    ```xml
    <mvc:resources mapping="swagger-ui.html" location="classpath:/META-INF/resources/"/>
    <mvc:resources mapping="/webjars/**" location="classpath:/META-INF/resources/webjars/"/>
    ```

  - 方式二

    ```xml
    <mvc:default-servlet-handler />
    ```

  *方式区别参考：* [https://www.cnblogs.com/dflmg/p/6393416.html]( https://www.cnblogs.com/dflmg/p/6393416.html) 

#### 配置配置类

```java
/**
 * 可以将bean注解到xml中，这样方便在正式环境中去掉Swagger <br>
 * 也可以配置Docket.enable属性
 */
@EnableSwagger2
@Configuration
public class SwaggerConfig {
    @Bean
    public Docket testApi(){
        return new Docket(DocumentationType.SWAGGER_2)
                .apiInfo(apiInfo())
                .enable(true) // 控制是否可用
                .select()
                .apis(RequestHandlerSelectors.withMethodAnnotation(ApiOperation.class))// 匹配给定注解的api
                .build();
    }

    private ApiInfo apiInfo(){
        return new ApiInfoBuilder()
                .title("TestSwaggerUI")
                .description("TestApiDocs")
                .termsOfServiceUrl("www.wangxiaonan.cn")
                .contact(new Contact("wxn","","wangxiaonan_0553@163.com"))
                .version("1.0")
                .build();
    }
}
```

- 建议将 bean 配置在xml等配置文件中，这样可以在生产环境容易去掉 swagger

- 也可以控制 Docket.enable 参数的形式去掉 swagger

- 可以通过注册多个 @Bean 对 api 进行分组，

  *参考：* [https://blog.csdn.net/w4hechuan2009/article/details/68892718]( https://blog.csdn.net/w4hechuan2009/article/details/68892718) 

- Docket 中有很多参数，可以参考下面的资料，

  *参考：* [https://github.com/springfox/springfox/blob/master/docs/transitioning-to-v2.md](https://github.com/springfox/springfox/blob/master/docs/transitioning-to-v2.md) 

#### Swagger 使用

- 启动访问 http://localhost:8080/swagger-ui.htm 可以看到 Swagger UI 的界面

  ![效果界面](/images/spring/springfox-swagger-ui.png) 

- swagger 注解

  | 作用范围       | API                | 使用位置                                                     |
  | -------------- | ------------------ | ------------------------------------------------------------ |
  | 协议集描述     | @Api               | 用于controller类上，表示标识这个类是swagger的资源            |
  | 协议描述       | @ApiOperation      | 用在controller的方法上，表示一个http请求的操作               |
  | 对参数         | @ApiParam          | 表示对参数的添加元数据（说明或是否必填等）                   |
  | 非对象参数集   | @ApiImplicitParams | 用在controller的方法上，表示单独的请求参数，可以是方法参数中没有的 |
  | 非对象参数描述 | @ApiImplicitParam  | 用在@ApiImplicitParams的方法里边                             |
  | 描述返回对象   | @ApiModel          | 用在返回对象类上，表示对类进行说明                           |
  | 对象属性       | @ApiModelProperty  | 用在出入参数对象的字段上，表示对model属性的说明或者数据操作更改 |
  | 协议描述       | @ApiIgnore         | 于类或者方法上，可以不被swagger显示在页面上                  |
  | Response集     | @ApiResponses      | 用在controller的方法上                                       |
  | Response       | @ApiResponse       | 用在 @ApiResponses里边                                       |

  ​

 *参考：* [https://github.com/swagger-api/swagger-core/wiki/Annotations]( https://github.com/swagger-api/swagger-core/wiki/Annotations) 

  	[https://blog.csdn.net/xupeng874395012/article/details/68946676](https://blog.csdn.net/xupeng874395012/article/details/68946676)

  

  参考工程地址：[https://github.com/wang-xiaonan/swagger-ui](https://github.com/wang-xiaonan/swagger-ui)

  

  #### 参考

  [Spring Boot中使用Swagger2构建强大的RESTful API文档 - 程序员DD](http://blog.didispace.com/springbootswagger2/) 

  [swagger2的常见注解，传递参数的注意使用方法](https://www.cnblogs.com/fengli9998/p/7921601.html) 