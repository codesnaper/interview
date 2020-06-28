# Interview

## Git
### **Merging v/s Rebasing**
So A user make a feature branch from master and another user push some of the changes to master branch which you are also working so in your file there will be confilct. This conflict can be solved by merging or rebasing.
So we can merge the master branch into the feature using command `git merge feature master`. <br>
Merging is nice because it’s a _non-destructive_ operation. The existing branches are not changed in any way<br>
So feature  branch will have an irrelevant  merge commit every time you need to incorporate upstream changes. If master is very active, this can pollute your feature branch’s history quite a bit. While it’s possible to mitigate this issue with advanced `git log` options, it can make it hard for other developers to understand the history of the project.<br>
<br>
Rebasing:<br>

### Question) Differnece between git statsh apply and git stash pop
git stash pop **removes the stash** (topmost) after applying it, whereas git stash apply **leaves it in the stash list** for possible later reuse.

### Question) Git fetch v/s git pull
git fetch  **imports commits from a remote repository into your local repo**. If you want to reflect these changes in your target branch, git fetch must be followed with a git merge. Since fetched content is represented as a remote branch, it has  absolutely  no effect on your local development work. This makes fetching a safe way to review commits before integrating them with your local repository. Your target branch will only be updated after merging the target branch and fetched branch. </br>

git pull does a git fetch followed by a git merge. 'git pull'  downloads  as well as merges the data from a remote repository into your local working files. It may also lead to merge conflicts if your local changes are not yet committed.
```git pull = git fetch + git merge```





## Spring 
### Spring MVC question:
#### What is a MultipartResolver and when its used?

Spring comes with  **MultipartResolver**  to handle  **file upload**  in web application. There are two concrete implementations included in Spring:
<br>
1.  **CommonsMultipartResolver**  for Jakarta Commons FileUpload
2.  **StandardServletMultipartResolver**  for Servlet 3.0 Part API
<br>
To define an implementation, create a bean with the id “**_multipartResolver_**” in a DispatcherServlet’s application context. Such a resolver gets applied to all requests handled by that DispatcherServlet.
<br>
If a  `DispatcherServlet`  detects a multipart request, it will resolve it via the configured  `MultipartResolver`  and pass on a wrapped HttpServletRequest. Controllers can then cast their given request to the  `MultipartHttpServletRequest`  interface, which permits access to any  `MultipartFiles`.

### Context-annotation Config v/s context: component-scan:
```
<context:annotation-config />
<bean id="beanA" class="com.howtodoinjava.beans.BeanA"></bean>
<bean id="beanB" class="com.howtodoinjava.beans.BeanB"></bean>
<bean id="beanC" class="com.howtodoinjava.beans.BeanC"></bean>
```

First we have discovered the beans using <bean> tags.
And anootation-config will simply inject the bean by activating @autowired.

context:component-scan:
```
<context:component-scan base-package="com.howtodoinjava.beans" />
```
It will automatically to both the job we dont have t discovered the bean it will automatically do that part. and also inject them.

### How to upload file in Spring MVC Application?

Let’s say we are going to use  **CommonsMultipartResolver**  which uses the Apache commons upload library to handle the file upload in a form. So you will need to add the  **commons-fileupload.jar**  and  **commons-io.jar**  dependencies.
pom.xml
```
<!-- Apache Commons Upload -->
<dependency>
    <groupId>commons-fileupload</groupId>
    <artifactId>commons-fileupload</artifactId>
    <version>1.2.2</version>
</dependency>
 
<!-- Apache Commons Upload -->
<dependency>
    <groupId>commons-io</groupId>
    <artifactId>commons-io</artifactId>
    <version>1.3.2</version>
</dependency>
```
The following declaration needs to be made in the application context file to enable the MultipartResolver (along with including necessary jar file in the application):
```
<bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
    <!-- one of the properties available; the maximum file size in bytes -->
    <property name="maxUploadSize" value="100000"/>
</bean>
```
Create Model:
```
import org.springframework.web.multipart.MultipartFile;
 
public class FileUploadForm 
{
    private MultipartFile file;
 
    public MultipartFile getFile() {
        return file;
    }
 
    public void setFile(MultipartFile file) {
        this.file = file;
    }
}
```
Create Controller:
```
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.ModelAttribute;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.multipart.MultipartFile;
import com.howtodoinjava.form.FileUploadForm;
 
@Controller
public class FileUploadController 
{
    @RequestMapping(value = "/upload", method = RequestMethod.POST)
    public String save(@ModelAttribute("uploadForm") FileUploadForm uploadForm, Model map) {
 
        MultipartFile multipartFile = uploadForm.getFile();
 
        String fileName = "default.txt";
 
        if (multipartFile != null) {
            fileName = multipartFile.getOriginalFilename();
        }
         
        //read and store the file as you like
 
        map.addAttribute("files", fileName);
        return "file_upload_success";
    }
}
```


## Spring Boot

### Spring boot v/s spring-mvc:
or example, if we are creating a web MVC application then including maven dependency  `spring-boot-starter-web`  only brings all jars/libraries used for building web, including RESTful, applications using Spring webMVC. Ut also includes Tomcat as the default embedded container.<br>

It also provides a range of non-functional features such as embedded servers, security, metrics, health checks, and externalized configuration out of the box without extra configurations.<br>

If we have to identify the difference between Spring framework and Spring boot, then we can say that Spring Boot is basically an extension of the Spring framework which eliminated the boilerplate configurations required for setting up a working production ready application.<br>

It takes an opinionated view of the Spring and third party libraries imported into project and configure the behavior for us. The difference is as simple as it.


### What is auto-configuration? How to enable or disable certain configuration?
Spring boot auto configuration scans the classpath, finds the libraries in the classpath and then attempt to guess the best configuration for them, and finally configure all such beans.
<br>
Auto-configuration tries to be as intelligent as possible and will back-away as we define more of our own custom configuration. It is always applied after user-defined beans have been registered.
<br>
Auto-configuration works with help of  **@Conditional**  annotations such as  `@ConditionalOnBean`  and  `@ConditionalOnClass`.
<br>
@ConditionalOnBean:<br>
```
@Configuration
public class ConditionalOnBeanConfig {

    @Bean
    public A beanA(){
        return new A();
    }
    
    @Bean
    @ConditionalOnBean(name="beanA")
    public B beanB(){
        return new B(); // it will initialize as beanA is present in the beanFactory.
    }
    
    @Bean
    @ConditionalOnBean
    public C beanC(){
        return new C(); // will not get initialized as there is no bean with return type C in BeanFactory.
    }
    
    @Bean
    public SimpleInt beanAInt(){
        return new ASimpleInt();
    }
    
    @Bean
    @ConditionalOnBean
    public SimpleInt beanBInt(){
        return new BSimpleInt();
    }
}
```
@ConditionalOnClass:
```
	@Configuration
public class ConditionOnClassConfig {

    @Bean
    @ConditionalOnClass(value={java.util.HashMap.class})
    public A beanA(){
        return new A(); // will get created as HashMap class is on the classpath
    }
    
    @Bean
    @ConditionalOnClass(name="com.sample.Dummy")
    public B beanB(){
        return new B(); // won't be created as Dummy class is not on classpath
    }
    
    @Bean
    @ConditionalOnClass(value=com.sample.bean.conditional.model.ASimpleInt.class)
    public C beanC(){
        return new C(); // ASimpleInt is on the classpath in the project. 
                        //So, C's instance will be created.
    }
    
}
```

@ConditionalOnMissingBean:
```
@Configuration
public class ConditionalOnMissingBeanConfig {

    @Bean
    public A beanA(){
        return new A(); // will initialize as normal
    }
    
    @Bean
    @ConditionalOnMissingBean(name="beanA")
    public B beanB(){
        return new B(); // it will not initialize as 
                        // beanA is present in the beanFactory.
    }
    
    @Bean
    @ConditionalOnMissingBean(name="beanD")
    public C beanC(){
        return new C(); // will get initialized as there is no 
                        // bean with name beanD in BeanFactory.
    }
   
}
```
@conditionalOnResource:
```
@Configuration
public class ConditionalOnResourceConfig {
    
    @Bean
    @ConditionalOnResource(resources={"classpath:application.properties"})
    public A beanA(){
        return new A(); // will initiate as application.properties is in 
                        // classpath.
    }

    @Bean
    @ConditionalOnResource(resources={"file:///e:/doc/data.txt"})
    public B beanB(){
        return new B(); // will not initialize as the file is not
                        // present in the given location.
    }
}
```
@ConditionalOnProperty:
```
@Configuration
public class ConditionalBeanPropertyConfig {
    
    @Bean
    @ConditionalOnProperty(name="test.property", havingValue="A")
    public A beanA(){
        return new A();
    }

    @Bean
    @ConditionalOnProperty(name="test.property", havingValue="B")
    public B beanB(){
        return new B();
    }
    
    @Bean
    @ConditionalOnProperty(name="test.property", havingValue="C",matchIfMissing=true)
    public C beanC(){
        return new C();
    }
}
```
### What are starter dependencies?

Spring Boot starters are maven templates that contain a collection of all the relevant transitive dependencies that are needed to start a particular functionality.
<br>
For example, If we want to create a  [Spring WebMVC](https://howtodoinjava.com/spring-boot2/rest/rest-api-example/)  application then in a traditional setup, we would have included all required dependencies ourselves. It leaves the chances of version conflict which ultimately result in more runtime exceptions.
<br>
With Spring boot, to create web MVC application, all we need to import is  `[spring-boot-starter-web](https://github.com/spring-projects/spring-boot/blob/master/spring-boot-project/spring-boot-starters/spring-boot-starter-web/pom.xml)`  dependency. Transitively, it brings in all other required dependencies to build a web application e.g. spring-webmvc, spring-web, hibernate-validator, tomcat-embed-core, tomcat-embed-el, tomcat-embed-websocket, jackson-databind, jackson-datatype-jdk8, jackson-datatype-jsr310 and jackson-module-parameter-names.

### 7. Why we use spring boot maven plugin?
It provides Spring Boot support in Maven, letting us package executable jar or war archives and run an application “in-place”. To use it, we must use Maven 3.2 (or later).
<br>
The  [plugin](https://docs.spring.io/spring-boot/docs/2.2.1.RELEASE/maven-plugin/usage.html)  provides several goals to work with a Spring Boot application:
<br>
-   `spring-boot:repackage`: create a jar or war file that is auto-executable. It can replace the regular artifact or can be attached to the build lifecycle with a separate  **classifier**.
-   `spring-boot:run`: run your Spring Boot application with several options to pass parameters to it.
-   `spring-boot:start`  and  `stop`: integrate your Spring Boot application to the  `integration-test`  phase so that the application starts before it.
-   `spring-boot:build-info`: generate a build information that can be used by the Actuator.

### 12. What is relaxed binding in Spring boot?

Spring Boot uses some relaxed rules for resolving configuration properties name such that a simple property name can be written in multiple ways.

For example, a simple property “log.level.my-package” can be written in following ways and all are correct and will be resolved by framework for it’s value based on property source.

`log.level.my-``package` `= debug` `//Kebab case`

`log.level.my_package = debug` `//Underscore notation`

`log.level.myPackage = debug` `//Camel case`

`LOG.LEVEL.MY-PACKAGE = debug` `//Upper case format`

Following is list of the relaxed binding rules per property source.

|PROPERTY SOURCE| TYPES ALLOWED |
|--|--|
| Properties Files | Camel case, kebab case, or underscore notation |
|YAML Files|Camel case, kebab case, or underscore notation|
|Environment Variables|Upper case format with underscore as the delimiter. `_` should not be used within a property name|
|System properties|Camel case, kebab case, or underscore notation|

### How to enable hot deployment and live reload on browser?
spring-boot-devtools


# Exception Handling
1. Clean Up Resources in a Finally Block or Use a Try-With-Resource Statement
2. Prefer Specific Exceptions
3. Document the Exceptions You Specify
4. Throw Exceptions With Descriptive Messages
5. Catch the Most Specific Exception First
6. Don’t Catch Throwable
7. Don't Ignore Exception
8. Don’t Log and Throw
9. Wrap the exception without consuming it


