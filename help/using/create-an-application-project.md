---
title: 建立AEM應用程式專案
seo-title: 建立AEM應用程式專案
description: 'null'
seo-description: 請依照本頁進一步瞭解如何在開始使用Cloud Manager時設定AEM專案。
uuid: 7b976ef-5358-49d8-a58 d-0bae026303 fa
contentOwner: jsyal
products: SG_ PERIENCENCENAGER/CLUDManager
topic-tags: 快速入門
discoiquuid: 76c1a8e4-d66 f-4a3 b-8c0 c-b80 c9 e17700 e
translation-type: tm+mt
source-git-commit: b39fc865e3c34052fb94b223d9eebc0fce3495d2

---


# Create an AEM Application Project {#create-an-aem-application-project}

## Using Wizard to Create an AEM Application Project {#using-wizard-to-create-an-aem-application-project}

當客戶登入Cloud Manager時，會提供空的git存放庫。目前的Adobe Managed Services(AMS)客戶(或移轉至AMS的內部AEM客戶)通常在其專案程式碼中已有其專案代碼(或其他版本控制系統)，並將其專案匯入Cloud Manager git儲存庫。不過，新客戶並沒有現有的專案。

為協助新客戶開始使用，Cloud Manger現在可以建立最少的AEM專案做為起點。This process is based on the [**AEM Project Archetype**](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype).

<!-- 

Comment Type: annotation
Last Modified By: jsyal
Last Modified Date: 2018-10-08T12:52:50.071-0400

2018.8.0: Added this new section

 -->

請依照下列步驟，在Cloud Manager中建立AEM應用程式專案：

1. Once you log in to Cloud Manager and the basic program setup is complete, a special call to action card will be shown on the **Overview** screen, if the repository is empty.

   ![](assets/image2018-10-3_14-29-44.png)

1. Click **Create** to navigate to the **Pipeline Setup** screen.

   ![](assets/image2018-10-3_14-30-22.png)

1. Click **Create to** open a dialog box, which allows the user to provide the parameters required by the AEM Project Archetype. 在預設表單中，對話方塊會要求兩個值：

   * **標題** -依預設，此項目會設為 *程式名稱*

   * **新分支名稱** -依預設此為 *主*
   ![](assets/screen_shot_2018-10-08at55825am.png)

   對話框中有一個抽屜，可以按一下對話框底部的控點來開啓。在擴充的表格中，對話方塊會顯示「Archetype」的所有組態參數。Many of these parameters have default values which are generated based on the **Title**.

   ![](assets/screen_shot_2018-10-08at60032am.png)

   >[!NOTE]
   >
   >For example, if the **Title** is ***We.Finance***, the Base Maven Artifact Id parameter is generated as ***com.wefinance***. 視需要變更這些值。
   >
   >
   >For example, you can change from the generated ***value com.wefinance*** to ***net.wefinance***.

1. Click **Create** in the preceding step to create the starter project by using the archetype and commit to the named git branch. 完成後，您就可以設定渠道。

## Setting up your Project {#setting-up-your-project}

### Modifying Project Setup Details {#modifying-project-setup-details}

若要透過Cloud Manager成功建立並部署，現有的AEM專案必須遵守一些基本規則：

* 專案必須使用Apache Maven建立。
* There must be a *pom.xml* file in the root of the Git repository. This *pom.xml* file can refer to as many submodules (which in turn may have other submodules, etc.) 視情況而定。

* You can add references to additional Maven artifact repositories in your *pom.xml* files. 不過，不支援存取受密碼保護或受網路保護的媒體儲存庫。
* Deployable content packages are discovered by scanning for content package *zip* files which are contained in a directory named *target*. 任何數量的子模組可能會產生內容封裝。

* Deployable Dispatcher artifacts are discovered by scanning for *zip* files (again, contained in a directory named *target*) which have directories named *conf* and *conf.d*.

* 如果有多個內容套件，則不保證套件部署的順序。如果需要特定順序，可以使用內容封裝相依性來定義順序。

<!-- 

Comment Type: annotation
Last Modified By: jsyal
Last Modified Date: 2018-10-08T09:20:10.106-0400

2018.8.0: added existing in the opening sentence

 -->

## Build Environment Details {#build-environment-details}

Cloud Manager builds and tests your code using a specialized build runtime **Environment**. 此環境具有下列屬性：

* 建置環境是以Linux為基礎。
* Apache Maven3.6.0已安裝。
* 安裝的Java版本為Oracle JDK8u202。
* 另外還安裝了一些安裝的系統套件：

   * bzip2
   * unzip
   * libpng
   * imagemaged
   * 圖形雜誌
   * 如果您需要其他套件，則需要透過客戶成功工程師(CSE)提出要求。

* 每個建置都是在原始環境上完成；組建容器不會保留執行之間的任何狀態。
* Maven is always run with the command: *mvn --batch-mode clean org.jacoco:jacoco-maven-plugin:prepare-agent package*
* Maven is configured at a system level with a settings.xml file which automatically includes the public Adobe **Artifact** repository. (Refer to [Adobe Public Maven Repository](https://repo.adobe.com/) for more details).

## Activating Maven Profiles in Cloud Manager {#activating-maven-profiles-in-cloud-manager}

在某些有限的情況下，在Cloud Manager內部執行時，您可能需要稍微變更組建程序，而不是在開發人員工作站上執行時。For these cases, [Maven Profiles](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) can be used to define how the build should be different in different environments, including Cloud Manager.

Activation of a Maven Profile inside the Cloud Manager build environment should be done by looking for the presence of an environment variable named `CM_BUILD`. 此變數一律會設定在Cloud Manager組建環境內。相反地，只想在Cloud Manager組建環境外部使用的描述檔，應尋找此變數的詳細資訊。

例如，如果您只想要在Cloud Manager內輸出簡單訊息，則您可以執行下列動作：

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
>To test this profile on a developer workstation, you can either enable it on the command line (with `-PcmBuild`) or in your Integrated Development Environment (IDE).

如果您只想在Cloud Manager以外的位置輸出簡單訊息，您可以這麼做：

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

## 自訂環境變數

在某些情況下，客戶的建置程序可能視特定組態變數而定，不適合放置在Git存放庫中。Cloud Manager允許客戶成功工程師(CSE)設定這些變數。這些變數會儲存在安全的儲存位置，並且僅會顯示在特定客戶的組建容器中。想要使用此功能的客戶需要聯絡其CSE來設定變數。

設定後，這些變數便可作為環境變數使用。In order to use them as a Maven properties，you can reference them in your loc file，possible within a profile as described above：

```xml
        <profile>
            <id>cmBuild</id>
            <activation>
                  <property>
                        <name>env.CM_BUILD</name>
                  </property>
            </activation>
            <properties>
                  <my.custom.property>${env.MY_CUSTOM_PROPERTY}</my.custom.property>  
            </properties>
        </profile>
```

>[!NOTE]
>
>環境變數名稱只能包含英數和底線(_)字元。依慣例，名稱應大寫。

## Develop your Code Based on Best Practices {#develop-your-code-based-on-best-practices}

Adobe Engineering and Consulting teams have developed a [comprehensive set of best practices for AEM developers](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/best-practices.html).
