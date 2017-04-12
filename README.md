MyBatis-Generator在Eclipse上配置及使用 
   之前用MyBatis框架的时候，都是手敲的代码，就感觉到好麻烦的样子。今天就到网上搜了一下MyBatis自动构建工具，就发现在官网上推荐了MyBatis Generator这个构建工具。官网推荐地址：http://mybatis.github.io/generator/index.html

         那接下来我就来详细介绍一下MyBatis Generator配置过程及其使用方法。

    MyBatis-Generator配置：
            1. 安装MyBatis-Generator插件

            1.1 首先，你得有MyBatis Generator这个插件。所以呢，离线安装MyBatis-Generator插件：                        下载地址：http://download.csdn.net/detail/wild_elegance_k/8999513

            1.2 安装MyBatis-Generator插件：

                       将下载的文件解压，将“features”、“plugins”拷贝到Eclipse的安装目录的相应目录中即可。

            2. MyBatis-Generator的使用：
    重启Eclipse，然后在项目中点右键，就能看到如图：







        新建一个generatorConfig.xml 之后呢，接下来就要我们来对其进行配置了，那先来说一说在这个xml 文件中主要的配置项有哪些，或者说哪些配置项是我们必须要填的。

            jdbcConnection --- 数据库链接URL、用户名、密码
            javaModelGenerator---生成模型的包名和位置，就是mybatis 里面用的一些entity 类的存放路径配置
            sqlMapGenerator ---生成的映射文件报名和位置，就是对应mybatis 的写sql 语句的xml文件的存放路径配置
            javaClientGenerator---生成DAO的包名和位置，就是mybatis 里面dao 接口的存放路径
            table ---这个配置项是配置在项目中操作的数据库表

        具体的配置的话，请看下面我的项目中的generator.xml：

        [html] view plain copy

            <?xml version="1.0" encoding="UTF-8" ?>  
            <!DOCTYPE generatorConfiguration PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN" "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd" >  
            <generatorConfiguration>  
                <!-- 数据库驱动包位置 -->  
                <classPathEntry  
                    location="D:\Applications\ProgrammingTools\maven\MavenRepository\mysql\mysql-connector-java\5.1.36\mysql-connector-java-5.1.36.jar" />  
                <context id="context1">  
                    <commentGenerator>  
                        <!-- 是否去除自动生成的注释 true：是 ： false:否 -->  
                        <property name="suppressAllComments" value="true"/>  
                    </commentGenerator>  
                    <!-- 数据库链接URL、用户名、密码 -->  
                    <jdbcConnection driverClass="com.mysql.jdbc.Driver"  
                        connectionURL="jdbc:mysql://localhost:3306/ssm1" userId="root" password="root" />  
                    <!-- 生成模型的包名和位置 -->  
                    <javaModelGenerator targetPackage="com.yc.ssm.cinema.entity" targetProject="Cinema/src/main/java" />  
                    <!-- 生成的映射文件报名和位置 -->  
                    <sqlMapGenerator targetPackage="com.yc.ssm.cinema.mapper" targetProject="Cinema/src/main/java" />  
                    <!-- 生成DAO的包名和位置 -->  
                    <javaClientGenerator targetPackage="com.yc.ssm.cinema.dao" targetProject="Cinema/src/main/java" type="XMLMAPPER" />  
                    <!-- 要生成的那些表(更改tableName 和domainObjectName 就可以了) -->  
                    <table schema="ssm1" tableName="FILMINFO" domainObjectName="FilmInfo" enableCountByExample="false" enableUpdateByExample="false"  
                        enableDeleteByExample="false" enableSelectByExample="false" selectByExampleQueryId="false">  
                        <columnOverride column="FILMID" property="FILMID" />  
                        <columnOverride column="FILMNAME" property="FILMNAME" />  
                        <columnOverride column="TYPEID" property="TYPEID" />  
                        <columnOverride column="ACTOR" property="ACTOR" />  
                        <columnOverride column="DIRECTOR" property="DIRECTOR" />  
                        <columnOverride column="TICKETPRICE" property="TICKETPRICE" />  
                    </table>  
                    <table tableName="FILMTYPE" domainObjectName="FiplType" enableCountByExample="false" enableUpdateByExample="false"  
                        enableDeleteByExample="false" enableSelectByExample="false" selectByExampleQueryId="false">  
                        <columnOverride column="TYPEID" property="TYPEID" />  
                        <columnOverride column="TYPENAME" property="TYPENAME" />  
                    </table>  
                </context>  
            </generatorConfiguration>  


        特别值得注意的是，一般我们用Eclipse的mybatis -generator插件时，都会是在项目中创建一个generatorConfig.xml 文件，所以在xml 文件中的targetProject="" 这一项需要配置的是项目的名字。但是我今天在配置时，我的项目名称叫Cinema，然后targetProject配置的targetProject="Cinema"，然而这并没有什么用，在配置好之后点下面的按钮时，程序一直都是显示运行成功，但是在项目的包结构中却迟迟不见文件。所以这个配置项需要特别值得注意，后来各种找解决办法，终于找到了正确的配置项：

        我就以javaModelGenerator配置为例：

        [html] view plain copy

            <javaModelGenerator targetPackage="com.yc.ssm.cinema.entity" targetProject="Cinema/src/main/java" />  

        这个配置就是指定targetProject的路径为Cinema项目下的src/main/Java包下面。


    MyBatis-Generator使用：

    配置好了之后，使用的时候就是一键操作的事：



    这个时候如果能看到配置项中指定的包不再为空时，就意味着generate成功了。





