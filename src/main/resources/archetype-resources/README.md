#set($symbol_pound = '#')
#set($symbol_dollar = '$')
#set($symbol_escape = '\')

${symbol_pound}${symbol_pound} ${artifactId} Java Project


This is ...

${symbol_pound} How to build and run

```shell
mvn clean assembly:assembly
java -jar target/${artifactId}-jar-with-dependencies.jar
```

${symbol_pound} How to create a customized archetype

In the root directory of project,
```shell
mvn archetype:create-from-project
```

update the generated source file on resource
修改骨架资源配置文件target/generated-sources/archetype/src/main/resources/META-INF/maven/archetype-metadata.xml, 用于创建空文件夹
```xml
<fileSets>
    <fileSet encoding="UTF-8">
      <directory>src/main/java</directory>
      <includes>
        <include>**/*.*</include>
      </includes>
    </fileSet>
    <fileSet encoding="UTF-8">
      <directory>src/main/resources</directory>
      <includes>
        <include>**/*.*</include>
      </includes>
    </fileSet>
    <fileSet encoding="UTF-8">
      <directory>src/test/java</directory>
      <includes>
        <include>**/*.*</include>
      </includes>
    </fileSet>
    <fileSet encoding="UTF-8">
      <directory>src/test/resources</directory>
      <includes>
        <include>**/*.*</include>
      </includes>
    </fileSet>
  </fileSets>
```
修改骨架名称，`target/generated-sources/archetype/pom.xml`

```xml
	<groupId>com.jackeylv.archetypes</groupId>
	<artifactId>maven-archetype-quickstart</artifactId>
	<version>1.0</version>
	<packaging>maven-archetype</packaging>
	<name>maven-archetype-quickstart</name>
```
安装到本地仓库
```shell
#进入到生成的骨架资源目录下
cd /target/generated-sources/archetype

#安装
mvn install

#更新本地骨架资源库文件
mvn archetype:update-local-catalog
```

使用骨架
```shell
#输入此命令根据提示选择骨架来创建项目
mvn archetype:generate -DarchetypeCatalog=local

#输入序号选择骨架，回车后根据提示继续
Choose archetype:
1: local -> com.jackeylv.archetypes:maven-archetype-webapp (maven-archetype-webapp)
2: local -> com.jackeylv.archetypes:maven-archetype-quickstart (maven-archetype-quickstart)
Choose a number or apply filter (format: [groupId:]artifactId, case sensitive contains): :
```