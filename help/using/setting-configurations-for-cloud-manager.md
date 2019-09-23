---
title: 為Cloud manager設定常規配置
seo-title: 設定Adobe AEM Cloud Manager的一般設定
description: 設定Cloud manager及從其使用者介面管理內容的先決條件。
seo-description: 設定Adobe AEM Cloud manager及從其使用者介面管理內容的先決條件。
uuid: 65d795f9-aa97-4816-b66b-03b5ae961f47
contentOwner: jsyal
discoiquuid: 03241b88-8d28-401b-aa42-17ead6183cd8
translation-type: tm+mt
source-git-commit: 093e25fa1cf2f5cdc3d8ea0bffd5c02ade854a88

---


# 設定常規配置 [!UICONTROL Cloud Manager]{#setting-up-general-configurations-for-cloud-manager}

以下章節重點說明從使用者介面 [!UICONTROL Cloud Manager] 設定和管理內容的必要條件。

本節頁面涵蓋下列主題

* **設定用戶和角色**
* **AEM應用程式專案設定**
* **Dispatcher Configurations**
* **開發最佳實務**

下圖說明可持續提供最佳品 [!UICONTROL Cloud Manager] 質程式碼的不同功能：

![](assets/screen_shot_2018-05-01at81926pm.png)

## 設定用戶和角色 {#setting-up-users-and-roles}

角色是從Adobe Admin [!UICONTROL Cloud Manager] Console管理的。 將使用者新增至「管理控制台」中的「產品設定檔」，即可 [!UICONTROL Cloud Manager] 提供特定角色成員資格。

>[!CAUTION]
>
>若要使 [!UICONTROL Cloud Manager]用，您必須擁有Adobe ID和Adobe Managed services產品內容。

您可以將使用者新增至「管理控制台」中的「產 [!UICONTROL Cloud Manager] 品設定檔」，以指派特定角色成員資格。

使用Admin Console建立下列角色 [!UICONTROL Cloud Manager]:

>[!NOTE]
>
>Adobe Admin Console可讓您集中管理整個組織的Adobe權益。
>
>若要進一步瞭解Adobe Admin Console，請參閱 [Admin Console的檔案](https://helpx.adobe.com/enterprise/using/admin-console.html)。

| **[!UICONTROL Cloud Manager]角色** | **說明** |
|---|---|
| 企業負責人 | 負責定義KPI、批准生產部署及覆寫重要的3層故障。 |
| 計畫經理 | 用於 [!UICONTROL Cloud Manager] 執行團隊設定、複查狀態和查看KPI。 可能會批准重要的3層故障。 |
| 部署管理員 | 管理部署操作。 用於 [!UICONTROL Cloud Manager] 執行階段／生產部署。 可能會批准重要的3層故障。 具備Git存取權。 |
| 開發人員 | 開發並測試自訂的應用程式碼。 主要用 [!UICONTROL Cloud Manager] 於查看狀態。 具有對Git的訪問權。 |
| 客戶成功工程師 | 通常支援AMS客戶的成功。 為執行需 [!UICONTROL Cloud Manager] 要CSE監督的部署而與之互動。 |
| 內容作者 | 通常不與互動 [!UICONTROL Cloud Manager]。 可能會使 [!UICONTROL Cloud Manager] 用Program Switcher(已瀏覽過 [!UICONTROL Experience Cloud])來存取AEM。 |

### 使用Admin console設定團隊 {#using-admin-console-to-set-up-team}

為了向用戶提供適當的基於角色的權 [!UICONTROL Cloud Manager] 限，客戶組織中的管理員必須在「產品上下文」下建立新的「產品 [!UICONTROL AEM Managed Services] 配置檔案」。

>[!NOTE]
>
>若要存取管理控制台並設定您的團隊（使用者和角色），請開啟瀏覽器並造訪 [https://adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise)。

將使用者（或群組）新增至這些產品設定檔是使用一般的管理控制台功能來完成，如下圖所示：

1. 登入管理控制台，然後按一下「 **新增描述檔** 」以新增描述檔。

   ![](assets/admin_console_roles.png)

1. 填寫欄位以設定新角色 [!UICONTROL Cloud Manager]。

   輸入 **配置檔案名**、 **說明** ，以建立新配置檔案。 此外，您也可以為描述 **檔選取「權限群組** 」。

   按一下「 **完成** 」(Done)以完成配置檔案建立步驟。

   ![](assets/screen_shot_2018-04-23at75014am.png)

## AEM應用程式專案設定 {#aem-application-project-setup}

在中設定應用程式項 [!UICONTROL Cloud Manager]目之前，您必須考慮兩個方案之一。 您可能是AEM 6.4的新手，或已是現有客戶。

>[!NOTE]
>
>若要存取，請連絡 [!UICONTROL Cloud Manager]客戶成功工程師(CSE)以取得URL和認證以開始使用。

您可以根據以下兩種方 [!UICONTROL Cloud Manager]案來設定應用程式項目：

* **新AEM專案**:

新的AEM專案將運用您現有的專案並搭配使用 [!UICONTROL Cloud Manager]。

如需詳細資訊，請 [參閱「AEM 6.4快速入門」](https://chl-author./content/help/en/experience-manager/6-4/sites/deploying/using/deploy.html)。 此外，請參閱 [AEM資源](https://www.adobe.com/marketing-cloud/experience-manager/resources.html?promoid=759X6WV8&mv=other) ，以取得詳細資訊。

* **現有AEM專案**:

現有的AEM專案必須向規則確認，才能設定專案。 您可以升級現有的AEM安裝，以取得AEM 6.4中提供的新功能和增強功能，並開始使用 [!UICONTROL Cloud Manager]。 這些准則應能在最小的變更下運作。 請聯絡客戶成功工程師(CSE)以取得支援。

若要取得有關將AEM例項升級至6.4的其他資訊，請參 [閱「升級至AEM 6.4」](https://helpx.adobe.com/experience-manager/6-4/sites/deploying/using/upgrade.html)。

### 設定儲存庫 {#setting-up-repository}

為已登錄的每個程式設定一個初始為空的Git儲存庫 [!UICONTROL Cloud Manager]。 開發人員和部署經理會從其CSE中取得git URL和認證。

有了這項資訊，開發人員可依照下節**專案設定**中的准則，新增其程式碼，以在使用前完成設定需求 [!UICONTROL Cloud Manager]。

## Dispatcher Configurations {#dispatcher-configurations}

[!UICONTROL Cloud Manager] 可部署Web伺服器和Dispatcher組態檔案（假設這些檔案儲存在git儲存庫中），以及一般的AEM內容封裝。

為了利用此功能，Maven構建版本將生成一個包含兩個目錄( ***conf*** 和 ***conf.d)的zip檔案***。

部署到調度器實例時，這些目錄的內容將覆蓋調度器實例上這些目錄的內容。 由於Web伺服器和調度程式配置檔案通常需要特定於環境的資訊，為了使此功能能夠正確使用，您首先需要與其客戶成功工程師(CSE)合作，將這些環境變數提取到/etc/sysconfig/httpd中。

按照以下步驟完成配置調度程式的初始過程：

1. 從其CSE獲取當前生產配置檔案。
1. 移除硬式編碼環境特定資料（例如發佈轉譯器IP），並以變數取代。
1. 在每個目標調度程式的鍵值對中定義所需的變數，並請求CSE在每個實例上添加到 ***/etc/sysconfig/httpd*** 。
1. 在舞台上測試更新的設定，然後要求CSE部署至生產環境，以確保其正常運作。
1. 將檔案提交到git。
1. 透過部署 [!UICONTROL Cloud Manager]。

實際的zip檔案可使用maven-assembly-plugin來製作。 使用Lazybones AEM Multimodule Template產生的專案可以建立正確的Maven專案結構，做為專案建立的一部分。

>[!NOTE]
>
>配置調度程式是在登錄過程中完成的， [!UICONTROL Cloud Manager]但也可以在以後的階段完成。

### 配置Dispatcher以進行效能測試 {#configuring-dispatcher-for-performance-testing}

為了正確 [!UICONTROL Cloud Manager] 運行效能測試，舞台調度器伺服器必須以與生產調度器一致的方式響應與生產調度器相同的主機名。

*例如*，如果客戶的生產主機名稱為 [www.myco.com](http://www.myco.com/) 和 [www.myotherco.com](http://www.myotherco.com,/) ，而stage-myco.adobecqms.net為其階段主機名稱，則此類請求必須正確回應：

```
curl -H"Host: www.myco.com" http://stage-myco.adobecqms.net/en/home.html
```

這不僅要求在分發程式配置中正確配置主機名，還要求以一致的方式在階段和生產階段之間實施 ***/etc/map***、任何Apache重寫或其他任何路徑 ****** 映射／過濾規則。

## 開發最佳實務 {#development-best-practices}

在使用 [!UICONTROL Cloud Manager]之前，建議您瞭解一些設定專案和設定Web伺服器或顯示設定的最佳實務。

### 專案設定 {#project-set-up}

您的專案必須符合某些標準才能使用 [!UICONTROL Cloud Manager]。

請遵循以下項目中設定專案的最佳實務 [!UICONTROL Cloud Manager]:

* 唯一提供並支援的建置工具是Apache Maven。 已安裝Apache Maven 3.3.9。
* 以root用戶身份在Docker容器的Linux環境中運行的構建。
* 安裝的Java版本是Oracle JDK 8u161。
* 另外還安裝了一些系統軟體包，如bzip2、unzip、libpng、imagemagick和graphicsmagick。 如果您需要其他套件，則需要透過CSE申請。
* Maven始終使用命令mvn -B clean軟體包運行。
* 您將只有一個Git儲存庫。 此儲存庫的根目錄中必須有pom.xml檔案。 此pom.xml檔案可以引用任意數量的子模組（這些子模組又可能具有其他子模組等）必要，但只有一個切入點。
* Maven在系統層級設定有設定。xml檔案，此檔案會自動包含公用Adobe工件存放庫(repo.adobe.com)。
* 您可以在pom.xml檔案中添加其他儲存庫。 但是，不支援對受密碼保護或受網路保護的對象儲存庫的訪問。
* 可部署的內容包是通過掃描名為target的目錄中包含的zip檔案來發現的。 同樣地，任何數量的子模組都可以生成內容包。
* 如果有多個內容包，則無法保證包部署的順序。 如果需要特定順序，則可使用內容包相關性來定義順序。

<!-- 

Comment Type: annotation
Last Modified By: jsyal
Last Modified Date: 2018-05-02T18:18:15.028-0400

change as per KT

 -->

### 後續步驟 {#the-next-steps}

一旦設定了常規配置，您就可以使用 [!UICONTROL Cloud Manager]。

請參 [閱使用[!UICONTROL Cloud Manager]](https://helpx.adobe.com/experience-manager/cloud-manager/using/using-cloud-manager.html) 以開始使用 [!UICONTROL Cloud Manager]。
