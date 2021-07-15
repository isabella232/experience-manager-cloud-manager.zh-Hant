---
title: 了解建置環境
description: 請詳閱本頁以了解環境
feature: 環境
exl-id: b3543320-66d4-4358-8aba-e9bdde00d976
source-git-commit: ee701dd2d0c3921455a0960cbb6ca9a3ec4793e7
workflow-type: tm+mt
source-wordcount: '999'
ht-degree: 0%

---

# 了解建置環境 {#build-environment-details}

Cloud Manager會使用專用的建置環境來建立和測試您的程式碼。 此環境具有下列屬性：

* 建置環境是以Linux為基礎，衍生自Ubuntu 18.04。
* 已安裝Apache Maven 3.6.0。
* 安裝的Java版本為OracleJDK 8u202、Azul Zulu 8u292、OracleJDK 11.0.2和Azul Zulu 11.0.11。
* 安裝了一些必需的附加系統軟體包：

   * bzip2
   * unzip
   * libpng
   * imagemagick
   * graphismagick

* 其他軟體包可在生成時安裝，如[下面所述](#installing-additional-system-packages)。
* 每棟建築都是在原始環境下建造的；建置容器不會在執行之間保留任何狀態。
* Maven一律使用下列三個命令執行：

   * `mvn --batch-mode org.apache.maven.plugins:maven-dependency-plugin:3.1.2:resolve-plugins`
   * `mvn --batch-mode org.apache.maven.plugins:maven-clean-plugin:3.1.0:clean -Dmaven.clean.failOnError=false`
   * `mvn --batch-mode org.jacoco:jacoco-maven-plugin:prepare-agent package`

* Maven在系統級別配置，具有settings.xml檔案，該檔案使用名為`adobe-public`的配置檔案自動包括公共Adobe **Artifact**儲存庫。
如需詳細資訊，請參閱[Adobe公用Maven存放庫](https://repo.adobe.com/) 。

>[!NOTE]
>雖然Cloud Manager未定義`jacoco-maven-plugin`的特定版本，但使用的版本至少必須為`0.7.5.201505241946`。


>[!NOTE]
>請參閱下列其他資源，了解如何使用Cloud Manager API:
> * [aio-cli-plugin-cloudmanager](https://github.com/adobe/aio-cli-plugin-cloudmanager)
>* [建立API整合](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/create-api-integration.md)
>* [API權限](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/permissions.md)


## 使用特定Java版本 {#using-java-version}

依預設，專案是由Cloud Manager建置程式使用Oracle8 JDK建置。 希望使用替代JDK的客戶有兩個選項：Maven工具鏈和為整個Maven執行過程選擇替代的JDK版本。

### Maven工具鏈 {#maven-toolchains}

[Maven工具鏈插件](https://maven.apache.org/plugins/maven-toolchains-plugin/)允許項目選擇特定JDK（或&#x200B;*工具鏈*），以用於工具鏈感知的Maven插件的上下文。 通過指定供應商和版本值，在項目的`pom.xml`檔案中完成此操作。 `pom.xml`檔案中的範例區段為：

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

這會導致所有工具鏈感知的Maven外掛程式都使用OracleJDK（第11版）。

使用此方法時，Maven本身仍使用預設的JDK(Oracle8)執行。 因此，透過外掛程式（例如[Apache Maven Enforcer Plugin](https://maven.apache.org/enforcer/maven-enforcer-plugin/)）檢查或強制執行Java版本時無法運作，因此不得使用這類外掛程式。

當前可用的供應商/版本組合包括：

* oracle1.8
* oracle1.11
* oracle11
* sun 1.8
* sun 1.11
* sun 11
* azul 1.8
* azul 1.11
* azul 8

### 備用Maven執行JDK版本 {#alternate-maven}

還可以選擇Azul 8或Azul 11作為JDK，以執行整個Maven執行。 與工具鏈選項不同，這會更改用於所有插件的JDK，除非還設定了工具鏈配置，在這種情況下，工具鏈配置仍應用於具有工具鏈的Maven插件。 因此，使用[Apache Maven Enforcer Plugin](https://maven.apache.org/enforcer/maven-enforcer-plugin/)檢查並強制執行Java版本將有效。

若要這麼做，請在管道使用的Git存放庫分支中建立名為`.cloudmanager/java-version`的檔案。 此檔案可包含內容11或8。 會忽略任何其他值。 如果指定了11，則使用Azul 11。 如果指定8，則使用Azul 8。

>[!NOTE]
>在Cloud Manager未來的版本中，預設JDK將被更改，預設JDK將為Azul 11。 不與Java 11相容的專案應盡快建立包含內容8的此檔案，以確保這些檔案不受此開關影響。


## 環境變數 {#environment-variables}

### 標準環境變數 {#standard-environ-variables}

在某些情況下，客戶會發現必鬚根據方案或管道的相關資訊來變更建置程式。

例如，如果正在執行建置時間JavaScript縮制，透過例如Gulp等工具，在建置開發環境時，可能會想使用不同的縮制層級，而非建置用於預備和生產。

為了支援此功能，Cloud Manager會將這些標準環境變數新增至每次執行的組建容器。

| **變數名稱** | **定義** |
|---|---|
| CM_BUILD | 一律設為「true」 |
| 分支 | 為執行配置的分支 |
| CM_PIPELINE_ID | 數值管線識別碼 |
| CM_PIPELINE_NAME | 管道名稱 |
| CM_PROGRAM_ID | 數值程式標識符 |
| CM_PROGRAM_NAME | 方案名稱 |
| ENTRACTS_VERSION | 對於階段或生產管道，由Cloud Manager產生的合成版本 |

### 管道變數 {#pipeline-variables}

某些情況下，客戶的建立程式可能取決於特定設定變數，這些變數不適合放置在Git存放庫中，或需使用相同分支在不同管道執行之間有所差異。

Cloud Manager允許透過Cloud Manager API或Cloud Manager CLI，依每個管道設定這些變數。 變數可儲存為純文字，或閒置時加密。 無論是哪種情況，變數都可在組建環境中作為環境變數使用，然後可從`pom.xml`檔案或其他組建指令碼內參照。

要使用CLI設定變數，請運行命令，如：

`$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test`

可列出目前的變數：

`$ aio cloudmanager:list-pipeline-variables PIPELINEID`

變數名稱只能包含英數字元和底線(_)字元。 按照慣例，名字應全部大寫。 若是字串類型變數，每個管道的變數數上限為200個，每個名稱必須少於100個字元，若是secretString類型變數，每個值必須少於2048個字元，若是secretString類型變數，則必須少於500個字元。

在`Maven pom.xml`檔案內使用時，使用類似下列的語法將這些變數對應至Maven屬性通常會很有幫助：

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

某些組建需要安裝額外的系統套件，才能完全運作。 例如，生成可以調用Python或ruby指令碼，因此需要安裝適當的語言解釋器。 若要這麼做，請呼叫[exec-maven-plugin](https://www.mojohaus.org/exec-maven-plugin/)以叫用APT。 此執行通常會包裝在Cloud Manager專屬的Maven設定檔中。 例如，要安裝python:

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

同樣的技術可用於安裝語言特定的軟體包，例如，對RubyGems使用`gem`，對Python軟體包使用`pip`。

>[!NOTE]
>以此方式安裝系統套件會&#x200B;**不**&#x200B;將其安裝在用於執行Adobe Experience Manager的執行階段環境中。 若您需要AEM環境上安裝系統套件，請連絡您的Adobe代表。
