
[TOC]

# 基本概念
坐标

依赖


Maven库


生命周期


插件

聚合

# 配置

```bash
# 代理第三方源
<mirrors>
<mirror>
 <id>nexus-aliyun</id>
 <mirrorOf>*</mirrorOf>
 <name>Nexus aliyun</name>
 <url>https://maven.aliyun.com/repository/public</url>
</mirror>
</mirrors>
```


继承
# 基本使用
```bash
mvn help:system    # 打印出所有java系统属性和环境变量

ping repo.maven.apache.org  # maven中央仓库

.m2/settings.xml  可设置代理

export MAVEN_OPTS="-Xms128m -Xmx512m"       # 

mvn archetype:generate         # 命令行生成maven框架
编译
mvn clean compile
mvn clean test
mvn clean package
mvn clean install
mvn clean install-U
mvn clean deploy

```

# 依赖

```bash
mvn dependency:list # 查看当前项目依赖 mvn dependency:tree mvn dependency:analyze

```

## 依赖范围(scope)

- 依赖范围就是来控制依赖与三种classpath(编译classpath, 测试classpath, 运行classpath)的关系

compile     # 编译依赖,(默认). 编译,测试,运行都有效
    test        # 测试依赖范围
    runtime     # 测试,运行有效,编译主代码无效
    provided    # 编译,测试有效, 运行无效
    system      # 和provided相同,但需要通过systemPath元素显示指定依赖文件的路径
    import      # 不会对三种classpath产生影响

## 传递性依赖

- 传递性依赖和依赖范围

```bash
compile	test	provided	runtime
compile	compile			runtime
test	test			test
provided	provided		provided	provided
runtime	runtime			runtime

```

- 依赖调节
路径最近者优先

第一声明者优先

## 可选依赖(optional)
## 排除依赖(exclusion)
## 归类依赖(properties)

# 仓库
仓库搜索服务
https://repository.sonatype.org/

http://mvnrepository.com/

http://mvnbrowser.com/

# 生命周期和插件
maven的生命周期是抽象的,其实际行为都有插件来完成
生命周期
生命周期: 项目的清理,初始化,编译,测试,打包,集成测试,验证,部署,站点生成

三套生命周期

clean
        pre-clean
        clean
        post-clean


    default
        process-sources: /src/main/resources  输出到classpath中
        compile:         /src/main/java
        process-test-sources:   src/test/resources
        test-compile:    src/test/java
        test
        package
        install
        deploy

    site
        pre-site
        site
        post-site
        site-deploy
插件绑定
内置绑定

自定义绑定

插件配置

命令行插件配置

mvn install -Dmaven.test.skip=true

全局配置

获取插件信息
在线插件信息
http://maven.apache.org/plugins/maven-compiler-plugin/plugins.html

使用maven-help-plugin描述插件

mvn help:describe -Dplugin=org.apache.maven.plugins:maven-compiler-plugin:2.1
mvn help:describe  -Dplugin = compiler -X
　插件解析机制

# pom聚合与继承
聚合 : 一条命令同时构建多个模块. 目的: 方便快速构建项目

继承 : 目的: 消除重复配置

依赖管理: dependencyManagement元素能让子模块继承到父模块的依赖配置,又能保证子模块依赖使用的灵活性

插件管理: pluginManagerment