一，修改banner

- 在创建的Springboot项目的resources资源文件夹下面，常见banner.txt。里面输入文字图案可以修改启动服务时显示的spring文字。

自动配置:

pom.xml

- spring-boot-dependencies：核心依赖在父工程中。
  - 单击spring-boot-starter-parent里面,我们在写或引入一些Springboot依赖的时候，不需要指定版本，就是因为有这些版本仓库。

启动器：

- ```
  <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-parent</artifactId>
  </dependency>
  ```

- springboot的启动器，比如spring-boot-starter-web会自动帮我们导入相关依赖。

主程序

@SpringBootApplication：注释表示s这个类是一个springboot的应用

8