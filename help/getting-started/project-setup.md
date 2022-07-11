---
title: 設定項目
description: 瞭解如何設定項目，以便您可以使用雲管理器管理和部署項目。
exl-id: ed994daf-0195-485a-a8b1-87796bc013fa
source-git-commit: 6572c16aea2c5d2d1032ca5b0f5d75ade65c3a19
workflow-type: tm+mt
source-wordcount: '1432'
ht-degree: 2%

---


# 項目設定 {#setting-up-your-project}

瞭解如何設定項目，以便您可以使用雲管理器管理和部署項目。

## 修改現有項目 {#modifying-project-setup-details}

現有AEM項目需要遵守一些基本規則，才能與Cloud Manager一起成功構建和部署。

* 必須使用Apache Maven生成項目。
* 一定有 `pom.xml` 檔案。
   * 此 `pom.xml` 檔案可以根據需要引用盡可能多的子模組（這些子模組又可能具有其他子模組）。
   * 您可以在中添加對其他Maven項目儲存庫的引用 `pom.xml` 的子菜單。
   * 訪問 [受密碼保護的項目儲存庫](#password-protected-maven-repositories) 配置時支援。 但是，不支援訪問受網路保護的項目儲存庫。
* 可部署的內容包是通過掃描目錄中包含的內容包.zip檔案來發現的 `target`。
   * 任意數量的子模組可以生成內容包。
* 可部署的Dispatcher對象通過掃描來發現 `zip` 檔案包含子目錄 `target` 命名 `conf` 和 `conf.d`。
* 如果有多個內容包，則無法保證包部署的順序。
* 如果需要特定訂單，則可以使用內容包依賴項來定義訂單。
* 包可能 [跳過](#skipping-content-packages) 從部署。

## 在雲管理器中激活Maven配置檔案 {#activating-maven-profiles-in-cloud-manager}

在某些有限情況下，在Cloud Manager內運行時，您可能需要稍微改變構建過程，而不是在開發人員工作站上運行。 對於這些案件， [馬文配置檔案](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) 可用於定義構建在不同環境（包括雲管理器）中的不同方式。

在Cloud Manager構建環境中激活Maven配置檔案應通過查找 `CM_BUILD` [環境變數](/help/getting-started/build-environment.md#environment-variables) 環境變數。 相反，應通過查找此變數的缺失來完成一個僅在Cloud Manager構建環境之外使用的配置檔案。

例如，如果您希望僅在在雲管理器內運行生成時才輸出一條簡單消息，則您將執行以下操作：

```xml
        <profile>
            <id>cmBuild</id>
            <activation>
                  <property>
                        <name>env.CM_BUILD</name>
                  </property>
            </activation>
            <build>
                <plugins>
                    <plugin>
                        <artifactId>maven-antrun-plugin</artifactId>
                        <version>1.8</version>
                        <executions>
                            <execution>
                                <phase>initialize</phase>
                                <configuration>
                                    <target>
                                        <echo>I'm running inside Cloud Manager!</echo>
                                    </target>
                                </configuration>
                                <goals>
                                    <goal>run</goal>
                                </goals>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
```

>[!NOTE]
>
>要在開發人員工作站上test此配置式，您可以在命令行上啟用它(使用 `-PcmBuild`)或整合開發環境(IDE)中。

如果您希望僅在生成在雲管理器之外運行時才輸出一條簡單消息，則您將執行以下操作：

```xml
        <profile>
            <id>notCMBuild</id>
            <activation>
                  <property>
                        <name>!env.CM_BUILD</name>
                  </property>
            </activation>
            <build>
                <plugins>
                    <plugin>
                        <artifactId>maven-antrun-plugin</artifactId>
                        <version>1.8</version>
                        <executions>
                            <execution>
                                <phase>initialize</phase>
                                <configuration>
                                    <target>
                                        <echo>I'm running outside Cloud Manager!</echo>
                                    </target>
                                </configuration>
                                <goals>
                                    <goal>run</goal>
                                </goals>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
```

## 受密碼保護的Maven儲存庫支援 {#password-protected-maven-repositories}

只有非常謹慎地使用受密碼保護的Maven儲存庫中的對象，因為通過此機制部署的代碼不會通過在Cloud Manager的質量門中實現的所有質量規則運行。 建議還部署Java源以及整個項目原始碼以及二進位代碼。

>[!TIP]
>
>密碼保護的Maven儲存庫中的對象只應用於極少數情況和未綁定到的代AEM碼。

要使用Cloud Manager中受密碼保護的Maven儲存庫，請將密碼（以及用戶名）指定為機密 [管線變數](/help/getting-started/build-environment.md#pipeline-variables) 然後在名為 `.cloudmanager/maven/settings.xml` 在git儲存庫中。 此檔案跟在 [Maven設定檔案](https://maven.apache.org/settings.html) 架構。

當Cloud Manager生成進程啟動時， `<servers>` 此檔案中的元素將合併到預設 `settings.xml` 由雲管理器提供的檔案。 伺服器ID以 `adobe` 和 `cloud-manager` 被視為保留，不應由自定義伺服器使用。 伺服器ID與這些前置詞之一或預設ID不匹配 `central` 將不會被雲管理器鏡像。

如果此檔案就位，將從 `<repository>` 和/或 `<pluginRepository>` 元素 `pom.xml` 的子菜單。 通常，這些 `<repository>` 和/或 `<pluginRepository>` 元素將包含在 [特定於雲管理器的配置檔案](#activating-maven-profiles-in-cloud-manager)儘管這並非嚴格必要。

例如，假設儲存庫位於 `https://repository.myco.com/maven2`，雲管理器應使用的用戶名為 `cloudmanager` 密碼是 `secretword`。

首先，將密碼設定為管道上的密碼：

```shell
$ aio cloudmanager:set-pipeline-variables PIPELINEID --secret CUSTOM_MYCO_REPOSITORY_PASSWORD secretword
```

然後從 `.cloudmanager/maven/settings.xml` 檔案：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd">
    <servers>
        <server>
            <id>myco-repository</id>
            <username>cloudmanager</username>
            <password>${env.CUSTOM_MYCO_REPOSITORY_PASSWORD}</password>
        </server>
    </servers>
</settings>
```

最後，引用 `pom.xml` 檔案：

```xml
<profiles>
    <profile>
        <id>cmBuild</id>
        <activation>
                <property>
                    <name>env.CM_BUILD</name>
                </property>
        </activation>
        <build>
            <repositories>
                <repository>
                    <id>myco-repository</id>
                    <name>MyCo Releases</name>
                    <url>https://repository.myco.com/maven2</url>
                    <snapshots>
                        <enabled>false</enabled>
                    </snapshots>
                    <releases>
                        <enabled>true</enabled>
                    </releases>
                </repository>
            </repositories>
            <pluginRepositories>
                <pluginRepository>
                    <id>myco-repository</id>
                    <name>MyCo Releases</name>
                    <url>https://repository.myco.com/maven2</url>
                    <snapshots>
                        <enabled>false</enabled>
                    </snapshots>
                    <releases>
                        <enabled>true</enabled>
                    </releases>
                </pluginRepository>
            </pluginRepositories>
        </build>
    </profile>
</profiles>
```

### 部署源 {#deploying-sources}

將Java源與二進位檔案一起部署到Maven儲存庫是一個很好的做法。

配置 `maven-source-plugin` 在項目中：

```xml
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-source-plugin</artifactId>
            <executions>
                <execution>
                    <id>attach-sources</id>
                    <goals>
                        <goal>jar-no-fork</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
```

### 部署項目源 {#deploying-project-sources}

將整個項目源與二進位檔案一起部署到Maven儲存庫是一個很好的做法。 這允許重建精確的工件。

配置 `maven-assembly-plugin` 在項目中：

```xml
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-assembly-plugin</artifactId>
            <executions>
                <execution>
                    <id>project-assembly</id>
                    <phase>package</phase>
                    <goals>
                        <goal>single</goal>
                    </goals>
                    <configuration>
                        <descriptorRefs>
                            <descriptorRef>project</descriptorRef>
                        </descriptorRefs>
                    </configuration>
                </execution>
            </executions>
        </plugin>
```

## 跳過內容包 {#skipping-content-packages}

在雲管理器中，生成可能會生成任意數量的內容包。 出於各種原因，可能希望生成內容包，但不部署它。 例如，在生成僅用於測試的內容包時或將通過生成過程中的另一個步驟重新打包的內容包（即作為另一包的子包）時，這可能很有用。

為了適應這些情況，Cloud manager將在內建內容包的屬性中 `cloudManagerTarget`查找名為 的屬性。如果此屬性設定為 `none`，將跳過並不部署包。 設定此屬性的機制取決於建立內容封裝的方式。例如， `filevault-maven-plugin` 您將按如下方式配置插件：

```xml
        <plugin>
            <groupId>org.apache.jackrabbit</groupId>
            <artifactId>filevault-package-maven-plugin</artifactId>
            <extensions>true</extensions>
            <configuration>
                <properties>
                    <cloudManagerTarget>none</cloudManagerTarget>
                </properties>
        <!-- other configuration -->
            </configuration>
        </plugin>
```

使用 `content-package-maven-plugin` 類似：

```xml
        <plugin>
            <groupId>com.day.jcr.vault</groupId>
            <artifactId>content-package-maven-plugin</artifactId>
            <extensions>true</extensions>
            <configuration>
                <properties>
                    <cloudManagerTarget>none</cloudManagerTarget>
                </properties>
        <!-- other configuration -->
            </configuration>
        </plugin>
```

## 生成項目重用 {#build-artifact-reuse}

在許多情況下，同一代碼會部署到多個AEM環境。 如果可能，當Cloud Manager檢測到多個完整堆棧管道執行中使用了相同的git提交時，將避免重建代碼庫。

啟動執行時，將提取分支管道的當前HEAD提交。 提交哈希在UI中和通過API可見。 當生成步驟成功完成時，生成的對象基於該提交哈希儲存，並且可以在後續管道執行中重用。

如果包位於同一程式中，則會在管道中重複使用。 在查找可重新使用的包時，AEM會忽略分支並重複使用對象。

當重用發生時，生成和代碼質量步驟被有效地替換為原始執行的結果。 生成步驟的日誌檔案將列出最初用於生成這些對象的執行資訊。

以下是此類日誌輸出的示例。

```shell
The following build artifacts were reused from the prior execution 4 of pipeline 1 which used commit f6ac5e6943ba8bce8804086241ba28bd94909aef:
build/aem-guides-wknd.all-2021.1216.1101633.0000884042.zip (content-package)
build/aem-guides-wknd.dispatcher.cloud-2021.1216.1101633.0000884042.zip (dispatcher-configuration)
```

代碼質量步驟的日誌將包含類似資訊。

### 範例 {#example-reuse}

#### 示例1 {#example-1}

請考慮您的計畫有兩個開發管道：

* 分支上的管線1 `foo`
* 分支上的管線2 `bar`

兩個分支都位於同一提交ID上。

1. 首先運行管道1將正常生成包。
1. 然後，運行管線2將重用由管線1建立的包。

#### 示例2 {#example-2}

請考慮您的計畫有兩個分支：

* 分支 `foo`
* 分支 `bar`

兩個分支具有相同的提交ID。

1. 開發管線生成並執行 `foo`。
1. 隨後生成並執行生產管線 `bar`。

在這個例子裡，那件藏物 `foo` 將重新用於生產管道，因為已標識同一提交哈希。

### 選擇退出 {#opting-out}

如果需要，可以通過設定管線變數來禁用特定管線的重用行為 `CM_DISABLE_BUILD_REUSE` 至 `true`。 如果設定了此變數，則仍會提取提交哈希，並且將儲存生成的對象以供以後使用，但不會重用以前儲存的任何對象。 要瞭解此行為，請考慮以下情形。

1. 將建立新管線。
1. 管線被執行(執行#1)，當前HEAD提交為 `becdddb`。 執行成功，並且會儲存結果對象。
1. 的 `CM_DISABLE_BUILD_REUSE` 變數已設定。
1. 管線在不更改代碼的情況下被重新執行。 儘管儲存了與 `becdddb`，由於 `CM_DISABLE_BUILD_REUSE` 變數。
1. 代碼被更改，管線被執行。 HEAD提交現在 `f6ac5e6`。 執行成功，並且會儲存結果對象。
1. 的 `CM_DISABLE_BUILD_REUSE` 變數已刪除。
1. 管線在不更改代碼的情況下被重新執行。 因為儲存了與 `f6ac5e6`，這些工件被重用。

### 警告 {#caveats}

* 生成對象不會在不同程式之間重複使用，而不管提交哈希是否相同。
* 即使分支和/或管線不同，生成對象也會在同一程式中重複使用。
* [Maven版本處理](/help/managing-code/maven-project-version.md) 僅在生產管道中替換項目版本。 因此，如果在開發部署執行和生產管道執行中都使用相同的提交，並且首先執行開發部署管道，則版本將部署到存放和生產中而不會更改。 但是，在這種情況下仍將建立標籤。
* 如果檢索所儲存的對象未成功，將執行生成步驟，就像沒有儲存對象一樣。
* 管道變數(非 `CM_DISABLE_BUILD_REUSE` 當Cloud Manager決定重新使用以前建立的生成對象時，不會考慮。

## 根據最佳做法制定您的代碼 {#develop-your-code-based-on-best-practices}

Adobe工程和咨詢團隊已開發了 [為開發人員提供一套全面的AEM最佳做法。](https://experienceleague.adobe.com/docs/experience-manager-65/developing/bestpractices/best-practices.html)
