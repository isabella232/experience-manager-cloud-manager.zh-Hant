---
title: 瞭解構建環境
description: 按照此頁瞭解環境
feature: Environments
exl-id: b3543320-66d4-4358-8aba-e9bdde00d976
source-git-commit: 9959f649e553d0ff6d41a70a468bec3e2e854d75
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 0%

---

# 瞭解構建環境 {#build-environment-details}

Cloud Manager使用專用的生成環境生成和test您的代碼。 此環境具有以下屬性：

* 構建環境基於Linux，源自Ubuntu 18.04。
* 已安裝Apache Maven 3.6.0。
* 安裝的Java版本是OracleJDK 8u202、Azul Zulu 8u292、OracleJDK 11.0.2和Azul Zulu 11.0.11。
* 預設情況下，JAVA_HOME環境變數設定為 `/usr/lib/jvm/jdk1.8.0_202` 包含OracleJDK 8u202。 請參閱 [備用Maven執行JDK版本](#alternate-maven) 的子菜單。
* 安裝了一些其他系統軟體包，這是必要的：

   * bzip2
   * 解壓縮
   * libpng
   * 影像
   * 圖形

* 其他軟體包可能會在生成時安裝，如所述 [下](#installing-additional-system-packages)。
* 每棟建築都是在原始環境下完成的；生成容器不會保留執行之間的任何狀態。
* Maven始終使用以下三個命令運行：

   * `mvn --batch-mode org.apache.maven.plugins:maven-dependency-plugin:3.1.2:resolve-plugins`
   * `mvn --batch-mode org.apache.maven.plugins:maven-clean-plugin:3.1.0:clean -Dmaven.clean.failOnError=false`
   * `mvn --batch-mode org.jacoco:jacoco-maven-plugin:prepare-agent package`

* Maven在系統級別配置了自動包括公共Adobe的settings.xml檔案 **藏物** 使用名為的配置檔案的儲存庫 `adobe-public`。
請參閱 [Adobe公共Maven儲存庫](https://repo1.maven.org/) 的子菜單。

>[!NOTE]
>雖然Cloud Manager未定義特定版本 `jacoco-maven-plugin`，使用的版本必須至少為 `0.7.5.201505241946`。


>[!NOTE]
>請參閱以下其他資源，瞭解如何使用Cloud Manager API:
> * [aio-cli-plugin-cloudmanager](https://github.com/adobe/aio-cli-plugin-cloudmanager)
>* [建立API整合](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/create-api-integration.md)
>* [API權限](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/permissions.md)


## 使用特定Java版本 {#using-java-version}

預設情況下，項目由Cloud Manager生成進程使用Oracle8 JDK生成。 希望使用備用JDK的客戶有兩個選項：Maven工具鏈，並為整個Maven執行進程選擇備用JDK版本。

### 馬文工具鏈 {#maven-toolchains}

的 [Maven工具鏈插件](https://maven.apache.org/plugins/maven-toolchains-plugin/) 允許項目選擇特定的JDK(或 *工具鏈*)。 在項目中完成 `pom.xml` 指定供應商和版本值。 中的示例部分 `pom.xml` 檔案為：

```xml
        <plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-toolchains-plugin</artifactId>
    <version>1.1</version>
    <executions>
        <execution>
            <goals>
                <goal>toolchain</goal>
            </goals>
        </execution>
    </executions>
    <configuration>
        <toolchains>
            <jdk>
                <version>11</version>
                <vendor>oracle</vendor>
            </jdk>
        </toolchains>
    </configuration>
</plugin>
```

這將導致所有支援工具鏈的Maven插件使用OracleJDK版本11。

使用此方法時，Maven本身仍使用預設JDK(Oracle8)和 `JAVA_HOME` 環境變數未更改。 因此，通過插件(如 [Apache Maven Enforcer插件](https://maven.apache.org/enforcer/maven-enforcer-plugin/) 不工作，因此不能使用此類插件。

當前可用的供應商/版本組合包括：

* oracle一點八
* oracle1.11
* oracle11
* 太陽1.8
* 週日1.11
* 11
* 藍色1.8
* 阿祖爾1.11
* 藍色

### 備用Maven執行JDK版本 {#alternate-maven}

也可以選擇Azul 8或Azul 11作為整個Maven執行的JDK. 與工具鏈選項不同，這將更改用於所有插件的JDK，除非還設定了工具鏈配置，在這種情況下，仍將對具有工具鏈意識的Maven插件應用工具鏈配置。 因此，使用 [Apache Maven Enforcer插件](https://maven.apache.org/enforcer/maven-enforcer-plugin/) 會奏效的。

為此，請建立名為 `.cloudmanager/java-version` 管道使用的git儲存庫分支中。 此檔案可以包含內容11或8。 忽略任何其他值。 如果指定了11，則使用Azul 11並將JAVA_HOME環境變數設定為 `/usr/lib/jvm/jdk-11.0.11`。 如果指定8，則使用Azul 8並將JAVA_HOME環境變數設定為 `/usr/lib/jvm/jdk-8.0.292`。

## 環境變數 {#environment-variables}

### 標準環境變數 {#standard-environ-variables}

在某些情況下，客戶發現有必要根據有關計畫或管道的資訊更改構建過程。

例如，如果正在執行生成時JavaScript小型化，則在構建開發環境時可能希望使用不同的小型化級別，而不是構建舞台和生產環境。

為支援此功能，Cloud Manager將這些標準環境變數添加到每次執行的生成容器中。

| **變數名稱** | **定義** |
|---|---|
| CM_BUILD | 始終設定為&quot;true&quot; |
| 分支 | 為執行配置的分支 |
| CM_PIPELINE_ID | 數字管道標識符 |
| CM_PIPELINE_NAME | 管線名稱 |
| CM_PROGRAM_ID | 數字程式標識符 |
| CM_PROGRAM_NAME | 程式名稱 |
| ARTACES_VERSION | 對於階段或生產管道，由Cloud Manager生成的合成版本 |

### 管道變數 {#pipeline-variables}

在某些情況下，客戶的構建過程可能取決於特定的配置變數，這些變數不適合放置在Git儲存庫中，或需要在使用同一分支的管道執行之間有所不同。

Cloud Manager允許通過Cloud Manager API或Cloud Manager CLI按管道配置這些變數。 變數可以以純文字檔案形式儲存，也可以以靜態方式加密。 在兩種情況下，變數都可在生成環境中作為環境變數使用，然後可以從 `pom.xml` 檔案或其他生成指令碼。

要使用CLI設定變數，請運行如下命令：

`$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test`

可列出當前變數：

`$ aio cloudmanager:list-pipeline-variables PIPELINEID`

變數名稱只能包含字母數字和下划線(_)字元。 按照慣例，名稱應全部為大寫。 每個管線有200個變數的限制，每個名稱必須少於100個字元，如果是字串類型變數，則每個值必須少於2048個字元，如果是secretString類型變數，則每個值必須少於500個字元。

當在 `Maven pom.xml` 檔案，通常使用類似以下語法將這些變數映射到Maven屬性會很有幫助：

```xml
        <profile>
            <id>cmBuild</id>
            <activation>
                <property>
                    <name>env.CM_BUILD</name>
                </property>
            </activation>
            <properties>
                <my.custom.property>${env.MY_CUSTOM_VARIABLE}</my.custom.property> 
            </properties>
        </profile>
```


## 安裝其他系統包 {#installing-additional-system-packages}

某些生成需要安裝其他系統軟體包才能完全運行。 例如，生成可以調用Python或ruby指令碼，因此需要安裝適當的語言解釋器。 通過調用 [exec-maven插件](https://www.mojohaus.org/exec-maven-plugin/) 調用APT。 此執行通常應包含在特定於雲管理器的Maven配置檔案中。 例如，要安裝python:

```xml
        <profile>
            <id>install-python</id>
            <activation>
                <property>
                        <name>env.CM_BUILD</name>
                </property>
            </activation>
            <build>
                <plugins>
                    <plugin>
                        <groupId>org.codehaus.mojo</groupId>
                        <artifactId>exec-maven-plugin</artifactId>
                        <version>1.6.0</version>
                        <executions>
                            <execution>
                                <id>apt-get-update</id>
                                <phase>validate</phase>
                                <goals>
                                    <goal>exec</goal>
                                </goals>
                                <configuration>
                                    <executable>apt-get</executable>
                                    <arguments>
                                        <argument>update</argument>
                                    </arguments>
                                </configuration>
                            </execution>
                            <execution>
                                <id>install-python</id>
                                <phase>validate</phase>
                                <goals>
                                    <goal>exec</goal>
                                </goals>
                                <configuration>
                                    <executable>apt-get</executable>
                                    <arguments>
                                        <argument>install</argument>
                                        <argument>-y</argument>
                                        <argument>--no-install-recommends</argument>
                                        <argument>python</argument>
                                    </arguments>
                                </configuration>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
```

同樣的技術可用於安裝語言特定的軟體包，即使用 `gem` 用於RubyGems或 `pip` Python包。

>[!NOTE]
>以此方式安裝系統軟體包確實 **不** 將其安裝到用於運行Adobe Experience Manager的運行時環境中。 如果需要在環境中安裝系統包AEM，請與Adobe代表聯繫。
