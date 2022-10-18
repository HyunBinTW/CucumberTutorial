Cucumber
===

大綱
---

- **開發環境**
    - IDE
    - Maven 
- **撰寫Scenario**
- **Run Cucumber**

***

###  開發環境

#### IDE : Spring Tool Suite 4 Version 4.16.0 
#### Maven 
```xml!

<!-- Cucumber -->
<dependency>
    <groupId>io.cucumber</groupId>
    <artifactId>cucumber-java</artifactId>
    <version>5.7.0</version>
    <scope>test</scope>
</dependency>
<dependency>
    <groupId>io.cucumber</groupId>
    <artifactId>cucumber-junit</artifactId>
    <version>5.7.0</version>
    <scope>test</scope>
</dependency>
<dependency>
    <groupId>io.cucumber</groupId>
    <artifactId>cucumber-spring</artifactId>
    <version>7.6.0</version>
    <scope>test</scope>
</dependency>
<dependency>
    <groupId>org.junit.vintage</groupId>
    <artifactId>junit-vintage-engine</artifactId>
    <version>5.7.0</version>
    <scope>test</scope>
</dependency>

<!-- assert -->
<dependency>
    <groupId>org.assertj</groupId>
    <artifactId>assertj-core</artifactId>
    <version>3.23.1</version>
    <scope>test</scope>
</dependency>
<dependency>
    <groupId>org.skyscreamer</groupId>
    <artifactId>jsonassert</artifactId>
    <version>1.5.0</version>
    <scope>test</scope>
</dependency>

<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <scope>test</scope>
</dependency>


```

#### Maven build

```xml!
<build>
<plugins>
<plugin>			<groupId>org.springframework.boot</groupId>
<artifactId>spring-boot-maven-plugin</artifactId>
</plugin>
<plugin>			<groupId>org.apache.maven.plugins</groupId>
<artifactId>maven-compiler-plugin</artifactId>
<configuration>
    <release>11</release>
</configuration>    
</plugin>
<plugin>			<groupId>org.apache.maven.plugins</groupId>
<artifactId>maven-surefire-plugin</artifactId> <version>3.0.0-M5</version> 
</plugin>        
</plugins>
</build>
```
***
###  撰寫Scenario

 

```
Feature為Scenario的集合

一個Scenario可以視為一個測試情境，

測試情境為一個以上的Step所組成，

撰寫Step會用到Gherkin的語法。


範例Scenario如下 :

Feature: 一句話簡介這份規格書所涵蓋的軟體功能
  對這份規格書更多的介紹 (非必要，不影響自動測試)
  介紹....
  介紹....

  Scenario: 要測試的測試案例 1
    Given 前提條件是....
    When 我做了某件事....
    Then 結果應該得到...

```

***
###  Run Cucumber

這邊會以OKD專案的測試為例子

#### RunnerTest.java
```
RunnerTest.java為測試的大門，

可以設置Cucumber的各項設定。

簡述有用到的Annotation

@RunWith-
基本上要跑Cucumber的測試，只能將設置為 "@RunWith(Cucumber.class)"

@CucumberOptions-	
features 設定要讀取的測試
glue	設定要讀取的Spring設定及Step及parameter
monochrome 設定可讀性

```

#### SpringIntegrationConfig.java
```
@SpringBootTest-
設定SpringBoot測試

@CucumberContextConfiguration
Cucumber針對Spring，需要加上此Annotation，以完成Spring的注入

@MockBean
MockBean需要在Spring啟動時注入，故如果要需要Mock的物件需在此初始化

```
#### ParameterTypeConfig
```
設定Step中讀取到特定字串的轉譯
OKD專案中是將字串類型的布林值轉換為布林
```