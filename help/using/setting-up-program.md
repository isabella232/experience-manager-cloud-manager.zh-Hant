---
title: 設定程式
seo-title: Set Up Your Program
description: 入職後，業務所有者需要對程式進行一些初始設定。
seo-description: After onboarding, the business owner will need to do some initial setup of Adobe AEM Cloud Manager. This involves setting the program description and defining the KPIs which will be used for performance testing.
feature: Getting Started
exl-id: 795c7112-d564-4fbf-96a1-152a6c286bf2
source-git-commit: 71d44c7e3673ca62fcd2203ecc0bc4ed9fa22002
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 1%

---

# 設定您的方案 {#setup-your-program}

登機後，業務所有者需要完成程式的一些初始設定。 這包括設定程式說明和定義用於效能測試的關鍵績效指標(KPI)。 也可以上載縮略圖。 此外，業務所有者可以在設定程式時配置環境配置。

定義的KPI用作每次管道執行時通過的效能測試的基線。

>[!NOTE]
>定義的KPI是按運行於 **階段** 環境。 通常，這些KPI會根據階段環境的功能進行縮放。
>例如，在生產中，平均每分鐘需要1000個頁面視圖的用戶 **環境** 而在生產中有四個dispatcher/publish伺服器時，應將此頁數量擴展到每分鐘250個頁面視圖（假定其階段環境僅包含一個dispatcher/publish伺服器對）。
>此外，許多用戶在其生產環境前面將有一個內容交付網路(CDN)，如Akamai或CloudFront。 自 [!UICONTROL Cloud Manager] test階段環境時，KPI應只反映預期通過CDN的流量，即快取未命中。 通常，這將是總生產流量中相對較小的子集。

## 使用 [!UICONTROL Cloud Manager] 設定程式 {#using-cloud-manager-to-setup-your-program}

按照以下步驟設定程式並定義KPI:

1. 按一下 **安裝程式** 在中啟動安裝進程 [!UICONTROL Cloud Manager]。

   ![影像1](assets/set-up-program/setup1.png)

   >[!NOTE]
   > 您始終可以從操作欄切換、編輯或添加新程式，如下圖所示。

   ![影像1](assets/set-up-program/setup2.png)


1. 的 **安裝程式** 螢幕顯示編輯程式資訊。

1. 您將看到三個選項 **常規**。 **KPI**, **設定** 頁籤。

1. 在 **常規** 頁籤，將縮略圖上載到您的程式。 您還可以向程式添加相關說明。

   ![](assets/Setup_Program-General.png)

1. 下 **KPI**，您可以定義兩個KPI（每個部署的期望值）。 為 **AEM Sites** 和 **AEM Assets**。 您將能夠指定已許可的產品的KPI。

   **AEM Sites**

   1. 您可以接受的第95百分位響應時間是多少？

      * 推薦值 — 3秒
   1. 在峰值負載下每分鐘頁面視圖數？

      * 推薦值 — 每分鐘200頁

   **AEM Assets**

   自最初發佈以來，Cloud Manager已能夠對AEM Sites程式執行效能測試。 在此版本中，還添加了執行AEM Assets程式效能test的功能。 資產效能測試是通過在30分鐘的test期間反複上載資產並測量每個資產的處理時間以及各種系統級度量來完成的。
在程式設定期間，指定特定於資產的KPI:

   * 第95百分位處理時間
   * 每分鐘上載的資產

   ![](assets/Setup_Program-KPIs.png)

1. 下 **設定**，您可以查看或編輯程式中生產和非生產環境的預配配置。 您將看到 **自動縮放已開啟**，如果已為程式啟用自動縮放。

   >[!NOTE]
   >自動縮放功能僅適用於生產環境，可能不適用於所有客戶計畫。

   ![](assets/Setup_Program-Provisioning.png)

1. 按一下 **保存** 的子菜單。

   >[!NOTE]
   >初始程式設定完成後，您始終可以編輯程式。 請按照以下步驟瞭解更多詳細資訊。

## 編輯程式 {#editing-program}

1. 從 **雲管理器** 主螢幕。

1. 按一下 **編輯程式** 從 **概述** 的下界。

   ![](assets/set-up-program/edit-program1.png)

1. 的 **編輯程式** 螢幕顯示，允許您更新或修改程式。

   您可以從 **常規** 頁籤。

   ![](assets/set-up-program/edit-program-general.png)

   導航到 **KPI** 頁籤，以更新有關AEM Sites和資產的資訊。

   ![](assets/set-up-program/edit-program-kpi.png)

   此外，您還可以導航到 **設定** 頁籤，編輯程式中生產和非生產環境的預配配置。

   ![](assets/set-up-program/edit-program-provision.png)

1. 按一下 **更新** 的子菜單。

## 後續步驟 {#the-next-steps}

如果已設定管道，則下次執行將考慮更新的設定。 如果尚未設定管道，請按照步驟先設定管道。

請參閱文檔 [配置生產管線](configuring-production-pipelines.md) 和 [配置非生產管道](configuring-non-production-pipelines.md) 來設定管道。
