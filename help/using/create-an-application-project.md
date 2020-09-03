---
title: 建立 AEM 應用程式專案
seo-title: 建立 AEM 應用程式專案
description: 'null'
seo-description: 請依照本頁進一步瞭解如何在Cloud Manager入門時設定AEM專案。
uuid: 7b976ebf-5358-49d8-a58d-0bae026303fa
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: getting-started
discoiquuid: 76c1a8e4-d66f-4a3b-8c0c-b80c9e17700e
translation-type: tm+mt
source-git-commit: c1d07c95088a279376ef495001a5165c7e459642
workflow-type: tm+mt
source-wordcount: '1861'
ht-degree: 6%

---


# 建立 AEM 應用程式專案 {#create-an-aem-application-project}

## 使用精靈建立AEM應用程式專案 {#using-wizard-to-create-an-aem-application-project}

當客戶已登入Cloud Manager時，他們會獲得一個空的git儲存庫。 目前的Adobe Managed Services(AMS)客戶（或內部部署AEM客戶，如果要移轉至AMS），通常其專案程式碼已位於git（或其他版本控制系統）中，並將其專案匯入Cloud Manager Git儲存庫。 但是，新客戶沒有現有的專案。

為協助新客戶開始使用，Cloud Manger現在可以建立最少的AEM專案作為起點。 此程式以 [**AEM Project Archetype為基礎**](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)。


請依照下列步驟，在Cloud Manager中建立AEM應用程式專案：

1. 一旦您登入Cloud Manager且基本程式設定完成後，如果儲存庫為空，「概述」畫面將會顯示特殊的動作卡呼叫。****

   ![](assets/image2018-10-3_14-29-44.png)

1. 按一 **下「建立** 」以開啟對話方塊，讓使用者提供AEM Project Archetype所需的參數。 在其預設形式中，對話框要求輸入兩個值：

   * **Title** —— 預設情況下，此設定為 *Program Name*

   * **新建分支名稱** -預設情況下，此為主分 *支*

   ![](assets/screen_shot_2018-10-08at55825am.png)

   對話框中有一個抽屜，可通過按一下指向對話框底部的手柄來開啟該抽屜。 在其展開形式中，對話框顯示Archetype的所有配置參數。 其中許多參數具有根據標題生成的預設 **值**。

   ![](assets/screen_shot_2018-10-08at60032am.png)

   >[!NOTE]
   >
   >例如，如果 **Title** is ***We.Finance***,Base Maven Artifact Id參數會產生 ***為com.wefinance***。 如有需要，這些值可以變更。
   >
   >
   >例如，您可以從產生的 ***值com.wefinance*** 變 ***更為net.wefinance***。

1. 按一 **下前述步驟中的** 「建立」，使用原型建立起始專案並提交至指定的git分支。 完成此操作後，可以設定管線。

## 設定專案 {#setting-up-your-project}

### 修改項目設定詳細資訊 {#modifying-project-setup-details}

若要使用Cloud Manager成功建立和部署現有的AEM專案，必須遵守一些基本規則：

* 必須使用Apache Maven建立專案。
* Git儲存庫 *的根目錄中必須有pom.xml* 檔案。 此 *pom.xml* 檔案可以引用任意數量的子模組（這些子模組又可能具有其他子模組等） 視需要。

* 您可以在 *pom.xml檔案中添加對其他Maven對象儲存庫的引* 用。 配置時 [支援對受密碼保護的對象儲存庫](#password-protected-maven-repositories) 的訪問。 但是，不支援對網路保護對象儲存庫的訪問。
* 可部署的內容套件是透過掃描內容套件 *zip* 檔案來發現的，這些檔案位於名為 *target的目錄中*。 任何數量的子模組都可以生成內容包。

* 可部署的Dispatcher對象是通過掃描 *zip檔案* (同樣，包含在名為target **&#x200B;的目錄中)來發現的，該目錄具有名為 *conf* 和 ** conf.d的目錄。

* 如果有多個內容包，則無法保證包部署的順序。 如果需要特定順序，則可使用內容包相關性來定義順序。 可從部署中 [跳過](#skipping-content-packages) 包。

<!-- 

Comment Type: annotation
Last Modified By: jsyal
Last Modified Date: 2018-10-08T09:20:10.106-0400

2018.8.0: added existing in the opening sentence

 -->

## 構建環境詳細資訊 {#build-environment-details}

Cloud Manager使用專業的構建環境來構建和測試代碼。 此環境具有以下屬性：

* 構建環境基於Linux，源自Ubuntu 18.04。
* 已安裝Apache Maven 3.6.0。
* 安裝的Java版本是Oracle JDK 8u202和11.0.2。
* 安裝了一些其他系統軟體包是必要的：

   * bzip2
   * unzip
   * libpng
   * imagick
   * graphicsmagick

* 其他軟體包可在構建時安裝，如下 [所述](#installing-additional-system-packages)。
* 每棟建築都是在原始環境下完成的；建置容器不會在執行之間保留任何狀態。
* Maven一律使用下列三個命令執行：

   * `mvn --batch-mode org.apache.maven.plugins:maven-dependency-plugin:3.1.2:resolve-plugins`
   * `mvn --batch-mode org.apache.maven.plugins:maven-clean-plugin:3.1.0:clean -Dmaven.clean.failOnError=false`
   * `mvn --batch-mode org.jacoco:jacoco-maven-plugin:prepare-agent package`

* Maven是在系統層級以settings.xml檔案來設定，該檔案會自動包含公用的Adobe **Artifact** 儲存庫。 (如需詳細 [資訊，請參閱Adobe Public Maven Repository](https://repo.adobe.com/) )。

>[!NOTE]
>雖然Cloud Manager未定義特定版本， `jacoco-maven-plugin`但使用的版本至少必須是 `0.7.5.201505241946`。

### 使用Java 11 {#using-java-11}

Cloud Manager現在支援使用Java 8和Java 11建立客戶專案。 依預設，專案是使用Java 8建立。 想要在專案中使用Java 11的客戶可使用 [Apache Maven Toolchains外掛程式](https://maven.apache.org/plugins/maven-toolchains-plugin/)。

若要這麼做，請在pom.xml檔案中新增 `<plugin>` 如下的項目：

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

>[!NOTE]
>支援的 `vendor` 值是 `oracle` 和，支 `sun` 援的值是 `version` 、 `1.8`和 `1.11``11`。

## 環境變數 {#environment-variables}

### 標準環境變數 {#standard-environ-variables}

在某些情況下，客戶會發現必鬚根據方案或管道的相關資訊來變更建立程式。

例如，如果正在執行建置時期的JavaScript精簡化，透過例如gulp等工具，在建立開發環境時，可能會想要使用不同的精簡化層級，而非建立舞台和生產環境。

為支援此功能，Cloud Manager會將這些標準環境變數新增至每個執行的建立容器。

| **變數名稱** | **定義** |
|---|---|
| CM_BUILD | 一律設為&quot;true&quot; |
| 分支 | 為執行配置的分支 |
| CM_PIPELINE_ID | 數值管線標識符 |
| CM_PIPELINE_NAME | 管線名稱 |
| CM_PROGRAM_ID | 數值程式標識符 |
| CM_PROGRAM_NAME | 程式名 |
| 對象_版本 | 對於舞台或生產管道，由Cloud Manager生成的合成版本 |

### 管線變數 {#pipeline-variables}

在某些情況下，客戶的構建過程可能取決於特定的配置變數，這些變數不適合放置在Git儲存庫中，或者需要使用同一分支在不同的管線執行之間有所不同。

Cloud Manager允許通過Cloud Manager API或Cloud Manager CLI按管道配置這些變數。 變數可儲存為純文字或在閒置時加密。 在這兩種情況下，變數都可在建立環境中做為環境變數使用，然後可從檔案或其他建立指令 `pom.xml` 碼中參考。

要使用CLI設定變數，請運行如下命令：

`$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test`

目前的變數可以列出：

`$ aio cloudmanager:list-pipeline-variables PIPELINEID`

變數名稱只能包含英數字元和底線(_)字元。 按照慣例，名稱應全部大寫。 每個管線有200個變數的限制，每個名稱必須小於100個字元，每個值必須小於2048個字元。

在檔案中使用時， `Maven pom.xml` 通常使用類似下列的語法將這些變數對應至Maven屬性會很有幫助：

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

## 在Cloud Manager中啟用Maven設定檔 {#activating-maven-profiles-in-cloud-manager}

在某些有限的情況下，在Cloud Manager內執行時，您可能需要稍微改變建立程式，而不是在開發人員工作站上執行。 在這些情況下， [Maven Profiles](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) 可用來定義在不同環境（包括Cloud Manager）中，建置應如何不同。

在Cloud Manager構建環境中激活Maven配置檔案時，應查找上述CM_BUILD環境變數。 轉換為，只能在Cloud Manager構建環境之外使用的配置檔案應通過查找此變數的基本含義來完成。

例如，如果您只想在Cloud Manager內執行組建時輸出簡單訊息，您可以執行下列動作：

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
>要在開發人員工作站上測試此配置檔案，可以在命令行(使用 `-PcmBuild`)或整合開發環境(IDE)中啟用它。

如果您只想在構建版本在Cloud Manager外部運行時輸出簡單消息，則可以執行以下操作：

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

>[!NOTE]
>使用密碼保護的Maven儲存庫中的對象只能非常謹慎地使用，因為透過此機制部署的代碼目前並未透過Cloud Manager的「品質門」執行。 因此，它只應用於少數情況，以及未系結至AEM的程式碼。 建議您也部署Java來源，以及整個專案原始碼與二進位檔。

若要使用Cloud Manager的受密碼保護的Maven儲存庫，請將密碼（以及使用者名稱）指定為機密 [Pipeline變數](#pipeline-variables) ，然後在git儲存庫中名為的檔案中參考 `.cloudmanager/maven/settings.xml` 該機密。 此檔案遵循「Maven [Settings File](https://maven.apache.org/settings.html) 」架構。 當Cloud Manager建置程式啟動時，此 `<servers>` 檔案中的元素將合併至Cloud Manager提 `settings.xml` 供的預設檔案。 伺服器ID從開 `adobe` 始， `cloud-manager` 並視為保留，不應由自訂伺服器使用。 Cloud Manager不 **會鏡像** ，也不會鏡像不符合其中 `central` 一個前置詞或預設ID的伺服器ID。 此檔案就位後，伺服器ID將會從檔案內 `<repository>` 的和/ `<pluginRepository>` 或元素 `pom.xml` 中參考。 通常，這 `<repository>` 些和／或 `<pluginRepository>` 元素會包含在 [Cloud Manager特定的配置檔案中](/help/using/create-an-application-project.md#activating-maven-profiles-in-cloud-manager)，儘管這並非嚴格的必要。

例如，假設儲存庫位於https://repository.myco.com/maven2,Cloud Manager應使用的用戶名為， `cloudmanager` 密碼為 `secretword`。

首先，將密碼設定為管道上的密碼：

`$ aio cloudmanager:set-pipeline-variables PIPELINEID --secret CUSTOM_MYCO_REPOSITORY_PASSWORD secretword`

然後，從檔案中參 `.cloudmanager/maven/settings.xml` 考此：

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

最後參考檔案中的伺服器 `pom.xml` ID:

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

### 部署來源 {#deploying-sources}

將Java源與二進位檔案一起部署到Maven儲存庫是一個很好的做法。

在您的專案中設定maven-source-plugin:

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

### 部署專案來源 {#deploying-project-sources}

將整個項目源與二進位檔案一起部署到Maven儲存庫是一個很好的做法——這樣可以重建確切的對象。

在您的專案中設定maven-assembly-plugin:

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

## 安裝其他系統軟體包 {#installing-additional-system-packages}

某些構建需要安裝其他系統軟體包才能完全運作。 例如，構建版本可以調用Python或ruby指令碼，因此需要安裝適當的語言解釋器。 若要這麼做，請呼 [叫exec-maven-plugin](https://www.mojohaus.org/exec-maven-plugin/) 以叫用APT。 此執行通常應包在Cloud Manager特定的Maven配置式中。 例如，要安裝python:

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

此相同技術可用於安裝語言特定的軟體包，即使用RubyGems或 `gem` Python軟體包 `pip` 進行安裝。

>[!NOTE]
>
>以此方式安裝系統套件 **不會** ，將它安裝在執行Adobe Experience Manager時所用的執行階段環境中。 如果您需要在AEM環境中安裝系統套件，請連絡您的客戶成功工程師(CSE)。

## 跳過內容包 {#skipping-content-packages}

在Cloud Manager中，組建可能會產生任意數量的內容套件。
由於各種原因，可能需要製作內容套件，但不要部署它。 例如，當建立僅用於測試的內容封裝時，或者在建立程式中的另一個步驟（即作為另一個封裝的子封裝）重新封裝的內容封裝時，這可能很有用。

為了適應這些情況，Cloud manager將在內建內容包的屬性中 ***查找名為cloudManagerTarget*** 的屬性。如果此屬性設定為none，則會跳過該包且不部署。設定此屬性的機制取決於建立內容封裝的方式。例如，使用filevault-maven-plugin時，您可以像這樣設定外掛程式：

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

使用content-package-maven-plugin時，其效果類似：

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

## 根據最佳實務來開發程式碼 {#develop-your-code-based-on-best-practices}

Adobe工程與諮詢團隊已針對AEM [開發人員開發一套完整的最佳實務](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/best-practices.html)。
