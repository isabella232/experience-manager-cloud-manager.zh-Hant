---
title: 設定專案
description: 請參閱本頁面，了解如何設定專案
feature: 快速入門，生產計畫
exl-id: ed994daf-0195-485a-a8b1-87796bc013fa
source-git-commit: cf19c7dfd593810779c03c51e08081954f8fc11e
workflow-type: tm+mt
source-wordcount: '877'
ht-degree: 8%

---

# 設定項目{#setting-up-your-project}

## 修改項目設定詳細資訊{#modifying-project-setup-details}

為了能順利透過Cloud Manager建立和部署，現有AEM專案必須遵循一些基本規則：

* 必須使用Apache Maven建立專案。
* Git存放庫的根目錄中必須有&#x200B;*pom.xml*&#x200B;檔案。 此&#x200B;*pom.xml*&#x200B;檔案可以引用許多子模組（而這些子模組又可能有其他子模組等） 視需要。

* 您可以在&#x200B;*pom.xml*&#x200B;檔案中新增對其他Maven工件存放庫的參考。 配置後，支援訪問[受密碼保護的對象儲存庫](#password-protected-maven-repositories)。 但是，不支援訪問受網路保護的對象儲存庫。
* 掃描名為&#x200B;*target*&#x200B;的目錄中包含的內容包&#x200B;*zip*&#x200B;檔案，可發現可部署的內容包。 任何數量的子模組都可產生內容包。

* 掃描名為&#x200B;*conf*&#x200B;和&#x200B;*conf.d*&#x200B;的&#x200B;*target*&#x200B;的目錄，可部署的Dispatcher成品即可發現。**

* 如果有多個內容包，則無法保證包部署的順序。 如果需要特定順序，則可使用內容套件相依性來定義順序。 可以從部署中跳過[](#skipping-content-packages)包。


## 在Cloud Manager中啟用Maven設定檔{#activating-maven-profiles-in-cloud-manager}

在某些有限的情況下，在Cloud Manager內執行時，您可能需要稍微改變您的建置程式，而不是在開發人員工作站上執行。 針對這些情況，[Maven設定檔](https://maven.apache.org/guides/introduction/introduction-to-profiles.html)可用來定義不同環境（包括Cloud Manager）中組建的差異。

請尋找上述的CM_BUILD環境變數，才能在Cloud Manager建置環境中啟動Maven設定檔。 相反地，如果設定檔僅用於Cloud Manager建置環境之外，則應尋找缺少此變數的情況，才能使用此設定檔。

例如，如果您只想在組建在Cloud Manager內執行時輸出簡單訊息，您可以執行以下操作：

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
>要在開發人員工作站上測試此配置檔案，可以在命令行(`-PcmBuild`)或在整合開發環境(IDE)中啟用它。

如果您只想在組建在Cloud Manager外部執行時輸出簡單訊息，您可以執行以下操作：

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

## 受密碼保護的Maven儲存庫支援{#password-protected-maven-repositories}

>[!NOTE]
>密碼保護的Maven存放庫中的成品使用時應非常謹慎，因為目前透過此機制部署的程式碼並未透過Cloud Manager的品質閘道執行。 因此，它只應用在少數情況下，以及不系結至AEM的程式碼。 建議您同時使用二進位檔來部署Java來源以及整個專案原始碼。

若要從Cloud Manager使用受密碼保護的Maven存放庫，請將密碼（以及選擇性的使用者名稱）指定為密碼[管道變數](/help/using/build-environment-details.md#pipeline-variables)，然後在Git存放庫中名為`.cloudmanager/maven/settings.xml`的檔案內參照該密碼。 此檔案遵循[Maven設定檔案](https://maven.apache.org/settings.html)架構。 當Cloud Manager建置程式開始時，此檔案中的`<servers>`元素將合併至Cloud Manager提供的預設`settings.xml`檔案。 以`adobe`和`cloud-manager`開頭的伺服器ID視為保留，自訂伺服器不應使用。 Cloud Manager不會鏡像符合其中一個前置詞或預設ID `central`的伺服器ID **。**&#x200B;使用此檔案後，將從`<repository>`和/或`<pluginRepository>`檔案內的`pom.xml`元素內引用伺服器ID。 通常，這些`<repository>`和/或`<pluginRepository>`元素會包含在[Cloud Manager特定設定檔](#activating-maven-profiles-in-cloud-manager)中，儘管這並非嚴格必要。

例如，假設存放庫位於https://repository.myco.com/maven2 ，則Cloud Manager應使用的使用者名稱為`cloudmanager` ，密碼為`secretword`。

首先，將密碼設為管道上的機密：

`$ aio cloudmanager:set-pipeline-variables PIPELINEID --secret CUSTOM_MYCO_REPOSITORY_PASSWORD secretword`

然後，從`.cloudmanager/maven/settings.xml`檔案中參考以下內容：

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

最後，參考`pom.xml`檔案內的伺服器ID:

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

### 部署源{#deploying-sources}

將Java來源與二進位檔一起部署至Maven存放庫是個不錯的作法。

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

### 部署項目源{#deploying-project-sources}

將整個專案來源與二進位檔一起部署至Maven存放庫是個不錯的作法，這樣就能重建確切的工件。

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

## 正在跳過內容包{#skipping-content-packages}

在Cloud Manager中，組建可能會產生任何數量的內容套件。
出於各種原因，可能需要製作內容包，但不要部署它。 例如，在建立僅用於測試的內容包時，這可能非常有用，或者，在構建過程中，將通過另一個步驟重新打包的內容包，即作為另一個包的子包。

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

使用content-package-maven-plugin時類似：

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

## 根據最佳實務{#develop-your-code-based-on-best-practices}開發您的程式碼

Adobe工程與諮詢團隊已為AEM開發人員開發一套[全面的最佳實務准則](https://helpx.adobe.com/tw/experience-manager/6-4/sites/developing/using/best-practices.html)。
