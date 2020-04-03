1.用IntelliJ IDEA 创建maven新项目；

2.maven添加mysql-connector-java依赖；pom.xml文件内容如下：
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>mys</groupId>
    <artifactId>mybatis.generator</artifactId>
    <version>1.0-SNAPSHOT</version>

    <dependencies>
        <!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>6.0.4</version>
        </dependency>

    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.mybatis.generator</groupId>
                <artifactId>mybatis-generator-maven-plugin</artifactId>
                <version>1.3.2</version>
                <configuration>
                    <verbose>true</verbose>
                    <overwrite>true</overwrite>
                </configuration>
            </plugin>
        </plugins>
    </build>

</project>

3.创建generatorConfig.xml；内容如下；连接数据库test，指定需要自动生成代码的表名 t_student;
<?xml version="1.0" encoding="UTF-8" ?>

<!DOCTYPE generatorConfiguration
        PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
        "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">

<generatorConfiguration>
    <!--数据库驱动路径-->
    <classPathEntry
            location="D:\gdyt-workspace-spring-cloud\my-project-work\mybatisgenerator\src\main\jar\mysql-connector-java-5.1.47.jar"/>
    <context id="DB2Tables" targetRuntime="MyBatis3">
        <commentGenerator>
            <property name="suppressAllComments" value="true"/>
        </commentGenerator>
        <jdbcConnection driverClass="com.mysql.jdbc.Driver"
                        connectionURL="jdbc:mysql://localhost/test"
                        userId="root" password="root">
        </jdbcConnection>
        <javaTypeResolver>
            <property name="forceBigDecimals" value="false"/>
        </javaTypeResolver>
        <!--域模型层,生成的目标包,项目目标源文件-->
        <javaModelGenerator targetPackage="com.mys.domain" targetProject="src/main/java">
            <property name="enableSubPackages" value="true"/>
            <property name="trimStrings" value="true"/>
        </javaModelGenerator>
        <!--XML映射文件,生成的位置（目标包）,源代码文件夹-->
        <sqlMapGenerator targetPackage="sqlmap" targetProject="src/main/resources">
            <property name="enableSubPackages" value="true"/>
        </sqlMapGenerator>
        <!--XML对应的Mapper类-->
        <javaClientGenerator type="XMLMAPPER" targetPackage="com.mys.mapper" targetProject="src/main/java">
            <property name="enableSubPackages" value="true"/>
        </javaClientGenerator>
        <!--下面是数据库表名和项目中需要生成类的名称，建议和数据库保持一致，如果有多个表，添加多个节点即可-->
        <table tableName="tbl_student" domainObjectName="Student" enableCountByExample="false" enableSelectByExample="false"
               enableUpdateByExample="false" enableDeleteByExample="false">
        </table>
    </context>
</generatorConfiguration>

4.用maven的插件生成代码；
![image](https://github.com/moyesen/myArticles/blob/master/image/maven-generator.jpg)
​​
5.生成的代码在src目录下；
![image](https://github.com/moyesen/myArticles/blob/master/image/generator-config.jpg)
