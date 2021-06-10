---
title: 設定您的方案
seo-title: 設定您的方案
description: 上線後，業務負責人將需要執行程式的一些初始設定。
seo-description: '上線後，業務擁有者將需要執行AdobeAEM Cloud Manager的一些初始設定。 這包括設定程式說明和定義用於效能測試的KPI。 '
feature: 快速入門
exl-id: 795c7112-d564-4fbf-96a1-152a6c286bf2
source-git-commit: a65c413e9ffa96f950cf1c59771b45ce0f810bc0
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 2%

---

# 設定您的方案 {#setup-your-program}

上線後，業務負責人需要完成程式的一些初始設定。 這包括設定程式說明和定義用於效能測試的關鍵績效指標(KPI)。 可選擇上傳縮圖。 此外，業務所有者可以在設定程式時配置環境配置。

定義的KPI可作為效能測試的基準，每次執行管道時都會傳遞此基準。

>[!NOTE]
>定義的KPI是在&#x200B;**stage**環境上執行的測試上測量。 通常，這些KPI會縮小以符合階段環境的功能。
>例如，如果使用者在生產&#x200B;**環境**中預期平均每分鐘1000次頁面檢視，且在生產中有四個Dispatcher/Publish伺服器，則應將此值縮放至每分鐘250次頁面檢視（假設其階段環境僅包含單一Dispatcher/Publish伺服器對）。
>此外，許多使用者在生產環境前會有內容傳遞網路(CDN)，例如Akamai或CloudFront。 由於[!UICONTROL Cloud Manager]會直接針對預備環境進行測試，因此KPI應僅反映預期要通過CDN的流量，亦即快取未命中。 這通常是生產流量總量中相對較小的子集。

## 使用[!UICONTROL Cloud Manager]設定程式{#using-cloud-manager-to-setup-your-program}

請依照下列步驟設定方案並定義KPI:

1. 按一下&#x200B;**Setup Program**&#x200B;以在[!UICONTROL Cloud Manager]中啟動安裝過程。

   ![image1](assets/set-up-program/setup1.png)

   >[!NOTE]
   > 您始終可以從操作欄切換、編輯或添加新程式，如下圖所示。

   ![image1](assets/set-up-program/setup2.png)


1. **Setup Program**&#x200B;螢幕顯示Edit Program Information。

1. 您會看到三個選項，如&#x200B;**一般**、**KPI**&#x200B;和&#x200B;**布建**&#x200B;標籤。

1. 在&#x200B;**一般**&#x200B;標籤中，將縮圖上傳至您的程式。 您也可以將相關說明新增至您的方案。

   ![](assets/Setup_Program-General.png)

1. 在&#x200B;**KPI**&#x200B;下，您可以定義兩個KPI（每個部署的預期值）。 分別為&#x200B;**AEM Sites**&#x200B;和&#x200B;**AEM Assets**&#x200B;定義KPI。 您將能指定您已授權產品的KPI。

   **AEM Sites**

   1. 您可接受的第95個百分位數回應時間是多少？

      * 建議值 — 3秒
   1. 峰值負載下每分鐘頁面檢視次數？

      * 建議值 — 每分鐘200次頁面檢視

   **AEM Assets**

   自首次發行以來，Cloud Manager已能夠執行AEM Sites程式的效能測試。 透過此版本，也新增了執行AEM Assets程式效能測試的功能。 資產效能測試的方式為在30分鐘的測試期間重複上傳資產，並測量每個資產的處理時間以及各種系統層級量度。
在程式設定期間，會指定資產專屬KPI:

   * 第95個百分位數處理時間
   * 每分鐘上傳資產

   ![](assets/Setup_Program-KPIs.png)

1. 在&#x200B;**預配**&#x200B;下，可以查看或編輯程式中生產和非生產環境的預配配置。 如果已為程式開啟了自動縮放功能，則會看到&#x200B;**自動縮放處於**&#x200B;上。

   >[!NOTE]
   >自動縮放功能僅適用於生產環境，可能不適用於所有客戶計畫。

   ![](assets/Setup_Program-Provisioning.png)

1. 按一下&#x200B;**Save**&#x200B;以完成安裝嚮導。

   >[!NOTE]
   >設定初始程式後，您隨時可以編輯程式。 請依照下列步驟以取得詳細資訊。

## 編輯方案

1. 導覽至&#x200B;**Cloud Manager**&#x200B;主畫面上的解決方案。

   ![](assets/SetUpProgram5.png)

1. 選擇解決方案，然後按一下&#x200B;**Edit**&#x200B;以更新或修改您的程式，如下圖所示。

   ![](assets/set-up-program/edit-program1.png)

1. 將顯示「**編輯程式**」螢幕，該螢幕允許您更新或修改程式。

   您可以從&#x200B;**General**&#x200B;頁簽更新程式名和說明。

   ![](assets/set-up-program/edit-program-general.png)

   導覽至&#x200B;**KPI**&#x200B;標籤，以更新AEM Sites和資產的相關資訊。

   ![](assets/set-up-program/edit-program-kpi.png)

   此外，您可以導航到&#x200B;**預配**&#x200B;頁簽，以編輯程式中生產和非生產環境的預配配置。

   ![](assets/set-up-program/edit-program-provision.png)

1. 按一下&#x200B;**更新**&#x200B;以儲存您的編輯。

## 後續步驟{#the-next-steps}

如果您已設定管道，則下次執行時會考量您更新的設定。 如果尚未設定管道，請依照步驟先設定管道。

請參閱[設定CI/CD管道](https://helpx.adobe.com/experience-manager/cloud-manager/using/configuring-pipeline.html)以設定管道。
