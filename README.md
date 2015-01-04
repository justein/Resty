resty 一款restful的轻量级的web框架
===========

拥有jfinal，activejdbc一样的activerecord的简洁设计，使用极其简单


独有有点：
restful的api设计，是作为restful的服务端最佳选择（使用场景：客户端和服务端解藕，用于对静态的html客户端（mvvm等），ios，andriod等提供服务端的api接口）

极简的route设计；
```java
  @GET("/users/:name")  在路径中自定义解析的参数 如果有其他符合 也可以用 /users/{name}
  //参数名就是方法变量名  除路径参数之外的参数也可以放在方法参数里  传递方式 user={json字符串}
  public Map find(String name,User user) { 
    //return Lister.of(name);
    return Maper.of("k1", "v1,name:" + name, "k2", "v2");//返回什么数据直接return，完全融入普通方法的方式
  }
```

支持多数据源和分布式事务（使用场景：需要访问多个数据库的应用，或者作为公司内部的数据中间件向客户端提供数据访问api等）

当然也是支持传统的web开发，你可以自己实现数据解析，在config里添加自定义的解析模板

```java
  public void configConstant(ConstantLoader constantLoader) {
    //通过后缀来返回不同的数据类型  你可以自定义自己的  render  如：FreemarkerRender
    //constantLoader.addRender("json", new JsonRender());//默认已添加json和text的支持，只需要把自定义的Render add即可
  }
```


运行example示例：

1.运行根目录下的pom.xml->install （把相关的插件安装到本地，稳定版之后发布到maven就不需要这样了）

2.在本地mysql数据库里创建demo,example数据库，对应application.properties的数据库配置

3.运行resty-example下的pom.xml->flyway-maven-plugin:migration，生成resources下得数据库表创建文件

4.运行resty-example下的pom.xml->tomcat7-maven-plugin:run,启动example程序

注意:推荐idea作为开发ide，使用分模块的多module开发


