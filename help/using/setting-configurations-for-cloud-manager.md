---
title: 設定Cloud Manager的一般設定
seo-title: 設定Adobe AEM Cloud Manager的一般設定
description: 設定Cloud Manager及從使用者介面管理內容的必要條件。
seo-description: 設定Adobe AEM Cloud Manager及從使用者介面管理內容的必要條件。
uuid: 65d795f9-aa97-4816-b66 b-03b5 ae961 f47
contentOwner: jsyal
discoiquuid: 0341b88-8d28-401b-aa42-17ead6183 cd8
translation-type: tm+mt
source-git-commit: 1dfb065c09569f811e5a006d3d74825d3bd7cc8d

---


# 設定一般設定 [!UICONTROL Cloud Manager]{#setting-up-general-configurations-for-cloud-manager}

下節重點說明從使用者介面設定 [!UICONTROL Cloud Manager] 及管理內容的必要條件。

本節頁面涵蓋下列主題

* **設定使用者和角色**
* **AEM應用程式專案設定**
* **Dispatcher組態**
* **開發最佳實務**

下圖說明可 [!UICONTROL Cloud Manager] 持續提供最佳品質代碼的不同函數：

![](assets/screen_shot_2018-05-01at81926pm.png)

## 設定使用者和角色 {#setting-up-users-and-roles}

角色是由 [!UICONTROL Cloud Manager] Adobe Admin Console管理。您可以在Admin Console中新增使用者至 [!UICONTROL Cloud Manager] 產品描述檔，以提供特定角色會籍。

>[!CAUTION]
>
>若要使用 [!UICONTROL Cloud Manager]，您必須擁有Adobe ID和Adobe Managed Services產品上下文。

您可以在管理控制台中新增使用者至 [!UICONTROL Cloud Manager] 產品描述檔，以指定特定角色會籍。

Create the following roles using the Admin console for [!UICONTROL Cloud Manager]:

>[!NOTE]
>
>Adobe Admin Console可讓您集中管理整個組織內的Adobe權益。
>
>若要進一步瞭解Adobe Admin Console，請參閱 [Admin Console的文件](https://helpx.adobe.com/enterprise/using/admin-console.html)。

| **[!UICONTROL Cloud Manager]角色** | **說明** |
|---|---|
| 企業負責人 | 負責定義KPI、核准生產部署並覆寫重要的層失敗。 |
| 方案經理 | 用於 [!UICONTROL Cloud Manager] 執行團隊設定、檢閱狀態及檢視KPI。可核准重要的層失敗。 |
| 部署管理員 | 管理部署作業。用於 [!UICONTROL Cloud Manager] 執行階段/生產部署。可核准重要的層失敗。擁有Git存取權。 |
| 開發人員 | 開發並測試自訂應用程式代碼。主要用於 [!UICONTROL Cloud Manager] 檢視狀態。已確認存取git。 |
| 客戶成功工程師 | 一般支援AMS客戶成功案例。與執行 [!UICONTROL Cloud Manager] 需要CSE監督的部署互動。 |
| 內容作者 | 通常不會與您互動 [!UICONTROL Cloud Manager]。可使用 [!UICONTROL Cloud Manager] Program Switcher(導覽自 [!UICONTROL Experience Cloud])存取AEM。 |

### 使用管理控制台來設定團隊 {#using-admin-console-to-set-up-team}

為了為 [!UICONTROL Cloud Manager] 使用者提供適當的角色權限，客戶組織中的管理員必須在 [!UICONTROL AEM Managed Services] 產品內容下建立新的產品描述檔。

>[!NOTE]
>
>若要呼叫管理主控台並設定您的團隊(使用者和角色)，請開啓瀏覽器並瀏覽 [https://adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise)。

將使用者(或群組)新增至這些「產品描述檔」是使用一般的「管理控制台」功能完成，如下圖所示：

1. 登入管理控制台，然後按一下 **「新增描述檔** 」以新增描述檔。

   ![](assets/admin_console_roles.png)

1. 填寫欄位以設定新角色 [!UICONTROL Cloud Manager]。

   輸入 **描述檔名稱**， **說明** 以建立新的描述檔。此外，您也可以選取描述檔 **的權限群組** 。

   按一下 **完成** ，完成描述檔建立步驟。

   ![](assets/screen_shot_2018-04-23at75014am.png)

## AEM應用程式專案設定 {#aem-application-project-setup}

在您設定應用程式專案之前 [!UICONTROL Cloud Manager]，您必須考慮這兩種情況之一。您可能是AEM6.4新手或現有客戶。

>[!NOTE]
>
>若要存取，請聯絡 [!UICONTROL Cloud Manager]客戶成功工程師(CSE)以取得開始使用的URL和認證。

您可以根據下列兩種情況 [!UICONTROL Cloud Manager]設定應用程式專案：

* **新的AEM專案**：

新的AEM專案將可運用您現有的專案 [!UICONTROL Cloud Manager]並搭配使用。

如需其他資訊，請參閱 [「AEM6.4快速入門](https://chl-author./content/help/en/experience-manager/6-4/sites/deploying/using/deploy.html)」。此外，請參閱 [AEM資源](https://www.adobe.com/marketing-cloud/experience-manager/resources.html?promoid=759X6WV8&mv=other) 以取得詳細資訊。

* **現有的AEM專案**：

現有的AEM專案必須確認規則至專案設定。您可以升級現有的AEM安裝，以取得AEM6.4中提供的新功能和增強功能 [!UICONTROL Cloud Manager]，並開始使用。這些准則必須最少變更。聯絡客戶成功工程師(CSE)以取得支援。

如需有關將AEM實例升級至6.4的額外資訊，請參閱 [升級至AEM6.4](https://helpx.adobe.com/experience-manager/6-4/sites/deploying/using/upgrade.html)。

### 設定儲存庫 {#setting-up-repository}

單一(最初是空白)的儲存空間會針對每個已登入的程式布 [!UICONTROL Cloud Manager]建。開發人員和部署經理會收到CID的URL和認證。

有了這項資訊，開發人員可以依照下面的成功區段中** Project Set Up**中的准則來新增他們的程式碼，以便在使用之前完成設定需求 [!UICONTROL Cloud Manager]。

## Dispatcher組態 {#dispatcher-configurations}

[!UICONTROL Cloud Manager] 除了一般的AEM內容封裝外，還可以部署Web伺服器和發送器組態檔，前提是它們儲存在Git存放庫中。

為善加利用此功能，Maven構建版本會產生包含兩個目錄( ***conf*** 和 ***conf. d***)的壓縮檔。

部署至dispatcher例項後，這些目錄的內容將會覆寫dispatcher例項上這些目錄的內容。由於網頁伺服器和調度器組態檔經常需要特定環境資訊，因此，您必須先與客戶成功工程師(CSE)合作，才能將這些環境變數擷取到/etc/sysconfig/httpd中。

請依照下列步驟完成設定發送器的初始程序：

1. 從CSE取得目前的生產設定檔案。
1. 移除硬式編碼環境專用資料(例如發佈轉譯器IP)並替換變數。
1. 為每個目標分派程式定義關鍵值配對中必要的變數，並要求CSE新增至 ***每個例項的/etc/sysconfig/httpd*** 。
1. 測試已更新的組態，然後要求CSE部署至生產環境，以確保它們正常運作。
1. 將檔案送出至Git。
1. 部署 [!UICONTROL Cloud Manager]。

實際zip檔案可使用maven-assembly-plugin產生。使用「lazybones AEM Multimodule範本」產生的專案可以使用建立專案的適當Maven專案結構。

>[!NOTE]
>
>設定發送器是在登入期間完成，但 [!UICONTROL Cloud Manager]也可以在稍後階段完成。

### 設定Dispatcher以進行效能測試 {#configuring-dispatcher-for-performance-testing}

為了正確執行效能測試， [!UICONTROL Cloud Manager] Stage Dispatcher伺服器必須以與生產伺服器一致的方式回應與生產發送器相同的主機名稱。

*例如*，如果客戶有 [www.myco.com](http://www.myco.com/) 和 [www.myotherco.com](http://www.myotherco.com,/) 作為其生產主機名稱和stage-myco. adobecqms. net作為其舞台主機名稱，則這類請求必須適當地回應：

```
curl -H"Host: www.myco.com" http://stage-myco.adobecqms.net/en/home.html
```

這不僅需要在dispatcher組態中正確設定主機名稱，還需要 ***/etc/map***、任何Apache重寫，或實際上任何其他路徑 ***對應/篩選*** 規則以一致方式建置階段和生產。

## 開發最佳實務 {#development-best-practices}

在使用 [!UICONTROL Cloud Manager]之前，建議您瞭解設定專案和設定網站伺服器或淨化組態的一些最佳實務。

### 專案設定 {#project-set-up}

您的專案必須遵守一些准則才能處理 [!UICONTROL Cloud Manager]。

請遵循設定專案的 [!UICONTROL Cloud Manager]最佳實務：

* 唯一提供和支援的建置工具是Apache Maven。Apache Maven3.3.9已安裝。
* 建立在Docker容器中的Linux環境中執行，做為root使用者。
* 安裝的Java版本為Oracle JDK8u161。
* 另外還安裝了一些額外的系統套件，例如bzip2、解壓縮、libpng、imagemaged和圖形標記。如果您需要其他套件，則需要透過CSE申請這些套件。
* Maven一律會使用命令mvn -B簡潔套件執行。
* 您將會提供一個Git存放庫。此存放庫的根目錄必須有pom.xml檔案。此pom.xml檔案可參照至多個子模組(依次為其他子模組等)。但必須有一個進入點。
* Maven是在系統層級設定的，settings.xml檔案會自動包含公開的Adobe網站存放庫(repo.adobe.com)。
* 您可以在pom.xml檔案中新增其他儲存庫。不過，不支援存取受密碼保護或受網路保護的媒體儲存庫。
* 可部署的內容封裝是透過掃描命名為目標目錄中的壓縮檔來發現。同樣地，任何數量的子模組都可能產生內容封裝。
* 如果有多個內容套件，則不保證套件部署的順序。如果需要特定順序，可以使用內容封裝相依性來定義順序。

<!-- 

Comment Type: annotation
Last Modified By: jsyal
Last Modified Date: 2018-05-02T18:18:15.028-0400

change as per KT

 -->

### 後續步驟 {#the-next-steps}

設定一般組態 [!UICONTROL Cloud Manager]後，您就可以使用。

請參閱 [「使用」[！UICOHTROL Cloud Manager]開始](https://helpx.adobe.com/experience-manager/cloud-manager/using/using-cloud-manager.html)[!UICONTROL Cloud Manager]使用。
