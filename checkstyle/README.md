# CheckStyle

checkstyle 是一个静态代码检查的工具，对 maven 和 gradle 有插件支持。

## maven-checkstyle-plugin

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">

    <properties>
        <maven-checkstyle-plugin.version>3.2.0</maven-checkstyle-plugin.version>
        <puppycrawl.checkstyle.version>10.5.0</puppycrawl.checkstyle.version>
    </properties>
  
    <build>
        <pluginManagement>
            <plugins>
                <plugin>
                    <groupId>org.apache.maven.plugins</groupId>
                    <artifactId>maven-checkstyle-plugin</artifactId>
                    <version>${maven-checkstyle-plugin.version}</version>
                    <configuration>
                        <configLocation>checkstyle/google_checks.xml</configLocation>
                        <consoleOutput>true</consoleOutput>
                        <failsOnError>true</failsOnError>
                        <failOnViolation>true</failOnViolation>
                    </configuration>
                    <dependencies>
                        <dependency>
                            <groupId>com.puppycrawl.tools</groupId>
                            <artifactId>checkstyle</artifactId>
                            <version>${puppycrawl.checkstyle.version}</version>
                        </dependency>
                    </dependencies>
                    <executions>
                        <execution>
                            <id>checkstyle-validation</id>
                            <!-- 绑定编译的生命周期：验证 -->
                            <phase>validate</phase>
                            <goals>
                                <!-- 在给定阶段执行的命令 -->
                                <goal>check</goal>
                            </goals>
                        </execution>
                    </executions>
                </plugin>
            
            </plugins>
        </pluginManagement>
    </build>

</project>
```

## checkstyle 参考文献

- 官网
  https://checkstyle.org
- google style's checkstyle
  - checkstyle-10.5.0 branch: https://github.com/checkstyle/checkstyle/blob/checkstyle-10.5.0/src/main/resources/google_checks.xml
  - master branch: https://github.com/checkstyle/checkstyle/blob/master/src/main/resources/google_checks.xml
  - 需要注意的是，这个 xml 配置文件的版本需要与 maven-checkstyle-plugin 中的 com.puppycrawl.tools中 dependency 的版本相同。对于 3.2 版本的 maven-checkstyle-plugin 使用的是 9.3 版本的 com.puppycrawl.tools 工具。 https://maven.apache.org/plugins/maven-checkstyle-plugin/examples/upgrading-checkstyle.html
