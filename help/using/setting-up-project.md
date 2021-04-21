---
title: 設定專案
description: 請依本頁瞭解如何設定專案
feature: 快速入門，製作程式
exl-id: ed994daf-0195-485a-a8b1-87796bc013fa
translation-type: tm+mt
source-git-commit: cf19c7dfd593810779c03c51e08081954f8fc11e
workflow-type: tm+mt
source-wordcount: '877'
ht-degree: 8%

---

# 設定您的專案{#setting-up-your-project}

## 修改項目設定詳細資訊{#modifying-project-setup-details}

為使用Cloud Manager成功建立和部署現有專案，AEM必須遵守一些基本規則：

* 必須使用Apache Maven建立專案。
* Git儲存庫的根目錄中必須有&#x200B;*pom.xml*&#x200B;檔案。 此&#x200B;*pom.xml*&#x200B;檔案可以引用許多子模組（這些子模組又可能具有其他子模組等） 視需要。

* 您可以在&#x200B;*pom.xml*&#x200B;檔案中添加對其他Maven對象儲存庫的引用。 配置時支援訪問[受密碼保護的對象儲存庫](#password-protected-maven-repositories)。 但是，不支援對網路保護對象儲存庫的訪問。
* 可部署的內容包是通過掃描內容包&#x200B;*zip*&#x200B;檔案來發現的，這些檔案包含在名為&#x200B;*target*&#x200B;的目錄中。 任何數量的子模組都可以生成內容包。

* 可部署的調度器對象通過掃描&#x200B;*zip*&#x200B;檔案（同樣，包含在名為&#x200B;*target*&#x200B;的目錄中）來發現，這些檔案具有名為&#x200B;*conf*&#x200B;和&#x200B;*conf.d*&#x200B;的目錄。

* 如果有多個內容包，則無法保證包部署的順序。 如果需要特定順序，則可使用內容包相關性來定義順序。 軟體包可以是部署中[跳過](#skipping-content-packages)的軟體包。


## 在Cloud Manager {#activating-maven-profiles-in-cloud-manager}中激活Maven配置檔案

在某些有限的情況下，在Cloud Manager內執行時，您可能需要稍微改變建立程式，而不是在開發人員工作站上執行。 對於這些情況，[Maven Profiles](https://maven.apache.org/guides/introduction/introduction-to-profiles.html)可用來定義不同環境（包括Cloud Manager）中構建版本的不同之處。

在Cloud Manager構建環境中激活Maven配置檔案時，應查找上述CM_BUILD環境變數。 相反地，應通過查找此變數的缺失來完成僅用於Cloud Manager構建環境以外的配置檔案。

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
>要在開發人員工作站上測試此配置檔案，可以在命令行（使用`-PcmBuild`）或整合開發環境(IDE)中啟用它。

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

## 受密碼保護的Maven儲存庫支援{#password-protected-maven-repositories}

>[!NOTE]
>使用密碼保護的Maven儲存庫中的對象只能非常謹慎地使用，因為透過此機制部署的代碼目前並未透過Cloud Manager的「品質門」執行。 因此，它只應用於極少數情況，以及不系結至程式碼AEM。 建議您也部署Java來源，以及整個專案原始碼與二進位檔。

若要使用Cloud Manager的受密碼保護的Maven儲存庫，請將密碼（以及使用者名稱）指定為機密[Pipeline變數](/help/using/build-environment-details.md#pipeline-variables)，然後在git儲存庫中名為`.cloudmanager/maven/settings.xml`的檔案中參考該機密。 此檔案遵循[Maven Settings File](https://maven.apache.org/settings.html)模式。 當Cloud Manager構建過程啟動時，此檔案中的`<servers>`元素將合併到Cloud Manager提供的預設`settings.xml`檔案中。 以`adobe`和`cloud-manager`開頭的伺服器ID會視為保留，自訂伺服器不應使用。 Cloud Manager將不會鏡像與其中一個前置詞或預設ID `central`匹配的伺服器ID **不**。 在此檔案就位後，將會從`<repository>`和／或`<pluginRepository>`檔案內的`pom.xml`元素中參考伺服器ID。 通常，這些`<repository>`和／或`<pluginRepository>`元素會包含在[雲端管理員專用的設定檔](#activating-maven-profiles-in-cloud-manager)中，但並非嚴格必要。

例如，假設儲存庫位於https://repository.myco.com/maven2,Cloud Manager應使用的用戶名為`cloudmanager` ，密碼為`secretword`。

首先，將密碼設定為管道上的密碼：

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

最後，請參考`pom.xml`檔案中的伺服器ID:

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

### 部署Project Sources {#deploying-project-sources}

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

## 正在跳過內容包{#skipping-content-packages}

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

## 根據最佳實務{#develop-your-code-based-on-best-practices}開發您的程式碼

Adobe工程與諮詢團隊已為開發人員開發一套[完整的最佳AEM實務](https://helpx.adobe.com/tw/experience-manager/6-4/sites/developing/using/best-practices.html)。
