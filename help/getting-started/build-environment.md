---
title: 構建環境
description: 瞭解Cloud Manager用戶構建和test代碼的專用構建環境。
exl-id: b3543320-66d4-4358-8aba-e9bdde00d976
source-git-commit: 4c051cd1696f8a00d0278131c9521ad4dcb956a3
workflow-type: tm+mt
source-wordcount: '1044'
ht-degree: 1%

---


# 構建環境 {#build-environment}

瞭解Cloud Manager用戶構建和test代碼的專用構建環境。

## 環境詳細資訊 {#details}

Cloud Manager的生成環境具有以下屬性。

* 構建環境基於Linux，源自Ubuntu 18.04。
* 已安裝Apache Maven 3.6.0。
* 安裝的Java版本是OracleJDK 8u202和OracleJDK 11.0.2。
* 預設情況下， `JAVA_HOME`  環境變數設定為 `/usr/lib/jvm/jdk1.8.0_202` 包含OracleJDK 8u202。 請參閱一節 [備用Maven執行JDK版本](#alternate-maven) 的子菜單。
* 安裝了一些其他系統軟體包，這是必要的。
   * `bzip2`
   * `unzip`
   * `libpng`
   * `imagemagick`
   * `graphicsmagick`
* 其他軟體包可以在生成時安裝，如一節中所述 [安裝其他系統包。](#installing-additional-system-packages)
* 每棟建築都是在原始環境下完成的。 生成容器不會保留執行之間的任何狀態。
* Maven始終使用以下三個命令運行：
   * `mvn --batch-mode org.apache.maven.plugins:maven-dependency-plugin:3.1.2:resolve-plugins`
   * `mvn --batch-mode org.apache.maven.plugins:maven-clean-plugin:3.1.0:clean -Dmaven.clean.failOnError=false`
   * `mvn --batch-mode org.jacoco:jacoco-maven-plugin:prepare-agent package`
* Maven在系統級配置 `settings.xml` 檔案，該檔案自動包括使用名為「C.S.....」的配置檔案的公共Adobe項目儲存庫 `adobe-public`。
   * 請參閱 [Adobe公共Maven儲存庫](https://repo1.maven.org/) 的子菜單。

>[!NOTE]
>
>雖然Cloud Manager未定義特定版本 `jacoco-maven-plugin`，使用的版本必須至少為 `0.7.5.201505241946`。

>[!TIP]
>
>請參閱以下其他資源，瞭解如何使用Cloud Manager API:
>* [aio-cli-plugin-cloudmanager](https://github.com/adobe/aio-cli-plugin-cloudmanager)
>* [建立API整合](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/)
>* [API權限](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/permissions/)


## 使用特定Java版本 {#using-java-version}

預設情況下，項目由Cloud Manager生成進程使用Oracle8 JDK生成。 希望使用備用JDK的客戶有兩個選項。

* [馬文工具鏈](#maven-toolchains)
* [為整個Maven執行進程選擇備用JDK版本](#alternate-maven)

### 馬文工具鏈 {#maven-toolchains}

的 [Maven工具鏈插件](https://maven.apache.org/plugins/maven-toolchains-plugin/) 允許項目選擇特定的JDK（或工具鏈），以在具有工具鏈意識的Maven插件的上下文中使用。 在項目中完成 `pom.xml` 指定供應商和版本值。 中的示例部分 `pom.xml` 檔案為：

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

| 廠商 | 版本 |
|---|---|
| oracle | 1.8 |
| oracle | 1.11 |
| oracle | 11 |
| 太陽 | 1.8 |
| 太陽 | 1.11 |
| 太陽 | 11 |

>[!NOTE]
>
>從2022年4月開始，OracleJDK將是應用程式開發和操作的預設JDKAEM。 即使在Maven工具鏈中顯式選擇了替代選項，Cloud Manager的生成過程也會自動切換到使用OracleJDK。 請參閱 [4月份發行說明](/help/release-notes/2022/2022-4-0.md) 的上界。

### 備用Maven執行JDK版本 {#alternate-maven}

也可以選擇Oracle8或Oracle11作為整個Maven執行的JDK。 與工具鏈選項不同，這將更改用於所有插件的JDK，除非還設定了工具鏈配置，在這種情況下，仍將對具有工具鏈意識的Maven插件應用工具鏈配置。 因此，使用 [Apache Maven Enforcer插件](https://maven.apache.org/enforcer/maven-enforcer-plugin/) 會奏效的。

為此，請建立名為 `.cloudmanager/java-version` 管道使用的git儲存庫分支中。 此檔案可以包含 `11` 或 `8`。 忽略任何其他值。 如果 `11` 指定，使用Oracle11, `JAVA_HOME` 環境變數設定為 `/usr/lib/jvm/jdk-11.0.2`。 如果 `8` 指定，使用Oracle8並 `JAVA_HOME` 環境變數設定為 `/usr/lib/jvm/jdk1.8.0_202`。

## 環境變數 {#environment-variables}

### 標準環境變數 {#standard-environ-variables}

在某些情況下，您可能會發現有必要根據有關程式或管道的資訊更改生成過程。

例如，如果構建時間的JavaScript微型化是通過諸如gulp之類的工具完成的，則在構建開發環境時可能希望使用不同的微型化級別，而不是構建用於試運行和生產。

為支援此功能，Cloud Manager會為每個執行將標準環境變數添加到生成容器中。

| 變數名稱 | 說明 |
|---|---|
| `CM_BUILD` | 始終設定為 `true` |
| `BRANCH` | 為執行配置的分支 |
| `CM_PIPELINE_ID` | 數字管道標識符 |
| `CM_PIPELINE_NAME` | 管線名稱 |
| `CM_PROGRAM_ID` | 數字程式標識符 |
| `CM_PROGRAM_NAME` | 程式名稱 |
| `ARTIFACTS_VERSION` | 對於暫存或生產管道，由Cloud Manager生成的合成版本 |

### 管道變數 {#pipeline-variables}

在某些情況下，您的生成過程可能取決於特定的配置變數，這些變數不適合放置在Git儲存庫中，或需要在使用同一分支的管道執行之間有所不同。

Cloud Manager允許通過Cloud Manager API或Cloud Manager CLI按管道配置這些變數。 變數可以以純文字檔案形式儲存，也可以以靜態方式加密。 在兩種情況下，變數都可在生成環境中作為環境變數使用，然後可以從 `pom.xml` 檔案或其他生成指令碼。

要使用CLI設定變數，請運行類似以下命令的命令。

```shell
$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test
```

可以使用類似於以下命令列出當前變數。

```shell
$ aio cloudmanager:list-pipeline-variables PIPELINEID
```

變數必須遵循某些限制。

* 變數名稱只能包含字母數字字元和下划線(`_`)。
   * 按照慣例，名稱應全部大寫。
* 每個管線有200個變數的限制。
* 每個名稱必須少於100個字元。
* 每個字串值必須少於2048個字元。
* 每個secretString值必須小於500個字元。

當在馬文內使用時 `pom.xml` 檔案中，使用類似以下語法將這些變數映射到Maven屬性通常會很有幫助。

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

為了充分運行，某些構建需要安裝額外的系統軟體包。 例如，生成可以調用Python或Ruby指令碼，因此需要安裝適當的語言解釋器。 通過調用 [`exec-maven-plugin`](https://www.mojohaus.org/exec-maven-plugin/) 調用APT。 此執行通常應包含在特定於雲管理器的Maven配置檔案中。 例如，要安裝Python:

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
>
>以這種方式安裝系統軟體包不會將其安裝在用於運行Adobe Experience Manager的運行時環境中。 如果需要在環境中安裝系統包AEM，請與Adobe代表聯繫。
