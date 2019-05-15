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
source-git-commit: 1dfb065c09569f811e5a006d3d74825d3bd7cc8d

---


# 建立AEM應用程式專案 {#create-an-aem-application-project}

## 使用精靈建立AEM應用程式專案 {#using-wizard-to-create-an-aem-application-project}

當客戶登入Cloud Manager時，會提供空的git存放庫。目前的Adobe Managed Services(AMS)客戶(或移轉至AMS的內部AEM客戶)通常在其專案程式碼中已有其專案代碼(或其他版本控制系統)，並將其專案匯入Cloud Manager git儲存庫。不過，新客戶並沒有現有的專案。

為協助新客戶開始使用，Cloud Manger現在可以建立最少的AEM專案做為起點。此程序以 [**AEM Project ArchetType**](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)為基礎。

<!-- 

Comment Type: annotation
Last Modified By: jsyal
Last Modified Date: 2018-10-08T12:52:50.071-0400

2018.8.0: Added this new section

 -->

請依照下列步驟，在Cloud Manager中建立AEM應用程式專案：

1. 當您登入Cloud Manager並完成基本程式設定後，如果存放庫空白， **「概述** 」畫面會顯示特殊的動作卡片呼叫。

   ![](assets/image2018-10-3_14-29-44.png)

1. 按一下 **「建立** 」以導覽 **至「管道設定」** 畫面。

   ![](assets/image2018-10-3_14-30-22.png)

1. 按一下 **「建立」** 開啓對話方塊，讓使用者提供AEM Project Archetype所需的參數。在預設表單中，對話方塊會要求兩個值：

   * **標題** -依預設，此項目會設為 *程式名稱*

   * **新分支名稱** -依預設此為 *主*
   ![](assets/screen_shot_2018-10-08at55825am.png)

   對話框中有一個抽屜，可以按一下對話框底部的控點來開啓。在擴充的表格中，對話方塊會顯示「Archetype」的所有組態參數。其中許多參數都具有根據 **標題產生的預設值**。

   ![](assets/screen_shot_2018-10-08at60032am.png)

   >[!NOTE]
   >
   >例如 **，如果「標題** 」為 ***「我們金融」***，則「基本遮色片Artifact ID」參數會產生 ***為com. webance***。視需要變更這些值。
   >
   >
   >例如，您可以從產生 ***的值com. webFinance*** 變更為 ***net. webance***。

1. 按一下前述步驟中 **的「建立」** ，以建立起始專案，方法是使用原型並提交給命名的git分支。完成後，您就可以設定渠道。

## 設定您的專案 {#setting-up-your-project}

### 修改專案設定詳細資訊 {#modifying-project-setup-details}

若要透過Cloud Manager成功建立並部署，現有的AEM專案必須遵守一些基本規則：

* 專案必須使用Apache Maven建立。
* Git存放庫的根目錄必須有 *pom.xml* 檔案。此 *pom.xml* 檔案可參照至多個子模組(依次為其他子模組等)。視情況而定。

* 您可以在 *pom.xml* 檔案中新增其他Maven Artifact儲存庫參照。不過，不支援存取受密碼保護或受網路保護的媒體儲存庫。
* 可部署的內容封裝是掃描內容封裝 ** 檔，方法是掃描名為 *目標目錄*中的內容封裝檔。任何數量的子模組可能會產生內容封裝。

* 部署可部署的Dispatcher偽象是掃描 *為****名為conf* 和 *conf. d*目錄的目錄(又包含在名為目標的目錄中)。

* 如果有多個內容套件，則不保證套件部署的順序。如果需要特定順序，可以使用內容封裝相依性來定義順序。

<!-- 

Comment Type: annotation
Last Modified By: jsyal
Last Modified Date: 2018-10-08T09:20:10.106-0400

2018.8.0: added existing in the opening sentence

 -->

## 建立環境詳細資訊 {#build-environment-details}

Cloud Manager使用專用的建置執行時期 **環境來建立並測試您的程式碼**。此環境具有下列屬性：

* 建置環境是以Linux為基礎。
* Apache Maven3.6.0已安裝。
* 安裝的Java版本為Oracle JDK8u181。
* 另外還安裝了一些安裝的系統套件：

   * bzip2
   * unzip
   * libpng
   * imagemaged
   * 圖形雜誌
   * 如果您需要其他套件，則需要透過客戶成功工程師(CSE)提出要求。

* Maven一律會使用命令執行： *mvn—批次模式clean org. jackoco：jacoco-maven-plugin：準備代理套件*
* Maven是在系統層級設定的，settings.xml檔案會自動包含公開的Adobe **Artifact** 存放庫。(請參閱 [Adobe Public Maven儲存庫以](https://repo.adobe.com/) 取得詳細資訊)。

## 在Cloud Manager中啓用Maven Profiles {#activating-maven-profiles-in-cloud-manager}

在某些有限的情況下，在Cloud Manager內部執行時，您可能需要稍微變更組建程序，而不是在開發人員工作站上執行時。在這些情況下 [，Maven Profiles](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) 可用來定義不同環境中的建置方式應如何不同，包括Cloud Manager。

在雲端管理員建立環境中啓用Maven Profile，應尋找是否 `CM_BUILD`存在環境變數。此變數一律會設定在Cloud Manager組建環境內。相反地，只想在Cloud Manager組建環境外部使用的描述檔，應尋找此變數的詳細資訊。

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
>若要在開發人員工作站上測試此描述檔，您可以在命令列上或在您的整合 `-PcmBuild`開發環境(IDE)上啓用此設定檔。

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

## 根據最佳實務開發您的程式碼 {#develop-your-code-based-on-best-practices}

Adobe工程與諮詢團隊已為AEM開發人員開發 [出一套完整的最佳實務](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/best-practices.html)。
