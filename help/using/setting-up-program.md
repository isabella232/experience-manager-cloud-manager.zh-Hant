---
title: 設定您的方案
seo-title: 設定您的方案
description: 上線後，企業負責人需要先設定程式。
seo-description: '上線後，企業負責人將需要進行Adobe AEM Cloud Manager的初始設定。 這包括設定方案說明，以及定義將用於效能測試的KPI。 '
uuid: 9ecf8743-1f5a-4744-86af-e2256567642f
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: getting-started
discoiquuid: c2393540-e852-4f7c-aafd-1427209065d2
translation-type: tm+mt
source-git-commit: 6851884b08c0c0a971242a958f72a7673a1a1196
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 2%

---


# 設定您的方案 {#setup-your-program}

上線後，企業負責人將需要完成程式的一些初始設定。 這包括設定方案說明，並定義將用於效能測試的關鍵績效指標(KPI)。 您也可以選擇上傳縮圖。 此外，業務所有者可以在設定程式時配置環境設定。

定義的KPI用作每次流水線執行時傳遞的效能測試基準。

>[!NOTE]
>
>定義的KPI是根據在舞台環境上執行的測 **試來測** 量。 通常，這些KPI會縮小以符合舞台環境的功能。
>
>例如，在生產環境中，平均每分鐘需要1000次頁面檢視，而在生產環境中有4個Dispatcher/publish伺服器的使用者，應將此值調整為每分鐘250次頁面檢視（假設其階段環境僅包含單一Dispatcher/publish伺服器對）。 ****
>
>此外，許多使用者在其製作環境前會有內容放送網路(CDN)，例如Akamai或CloudFront。 由於 [!UICONTROL Cloud Manager] 直接針對階段環境進行測試，因此KPI應僅反映預期要透過CDN的流量，即快取未命中。 通常，這是生產流量總量中相對較小的子集。

## 使用 [!UICONTROL Cloud Manager] 來設定程式 {#using-cloud-manager-to-setup-your-program}

請依照下列步驟設定方案並定義KPI:

1. 按一下 **Setup Program** （設定程式）以在中啟動設定過程 [!UICONTROL Cloud Manager]。

   ![image1](assets/set-up-program/setup1.png)

   >[!NOTE]
   > 您隨時都可以從動作列切換、編輯或新增程式，如下圖所示。

   ![image1](assets/set-up-program/setup2.png)


1. 「安 **裝程式** 」螢幕顯示「編輯程式資訊」。

1. 您將會看到三個選項 **:「一般**」、 **KPI**&#x200B;和「布 **建** 」標籤。

1. 在「一 **般** 」索引標籤中，將縮圖上傳至您的程式。 您也可以將相關說明新增至您的方案。

   ![](assets/Setup_Program-General.png)

1. 在 **KPI**&#x200B;下，您可以定義兩個KPI（每個部署的預期值）。 AEM Sites和 **AEM Assets會分別定義****KPI**。 您將可以指定已授權產品的KPI。

   **AEM Sites**

   1. 您可以接受的第95個百分位數回應時間是多少？

      * 建議值- 3秒
   1. 在高峰負載下，每分鐘頁面檢視次數是多少？

      * 建議值——每分鐘200次頁面檢視
   **AEM Assets**

   自從Cloud Manager初次推出以來，就可以執行AEM Sites程式的效能測試。 在此版本中，也新增了執行AEM Assets程式效能測試的功能。 資產效能測試是透過在30分鐘測試期間重複上傳資產，並測量每個資產的處理時間以及各種系統層級度量來完成。
在方案設定期間，會指定資產特定的KPI:

   * 第95個百分位數的處理時間
   * 每分鐘上傳的資產
   ![](assets/Setup_Program-KPIs.png)

1. 在「 **布建**」下，您可以查看或編輯程式中生產和非生產環境的布建配置。 如果已為程 **序開啟自動縮放**，您將看到自動縮放已開啟。

   >[!NOTE]
   >
   >* 自動縮放功能僅適用於生產環境，可能不適用於所有客戶程式。
   >* 此版本的不提供隨選縮放 [!UICONTROL Cloud Manager]。


   ![](assets/Setup_Program-Provisioning.png)

1. 按一 **下「儲存** 」以完成設定精靈。

   >[!NOTE]
   >
   >在初始程式設定完成後，您始終可以編輯程式。 請依照下列步驟來取得詳細資訊。

## 編輯程式

1. 導覽至 **Cloud Manager首頁畫面上的解決方案** 。

   ![](assets/SetUpProgram5.png)

1. 選擇解決方案，然後按一下「 **編輯** 」(Edit)以更新或修改程式，如下圖所示。

   ![](assets/SetUpProgram6.png)

1. 此時 **會顯示「編輯程式** 」螢幕，允許您更新或修改程式。

   ![](assets/Editing_Program-screen3.png)

## 後續步驟 {#the-next-steps}

如果您已經設定了 **Pipeline**，下次執行時將考慮您的更新設定。 如果尚未設定管線，請按照步驟先設定管線。

請參 [閱配置CI/CD管道](https://helpx.adobe.com/experience-manager/cloud-manager/using/configuring-pipeline.html) ，以設定管道。
