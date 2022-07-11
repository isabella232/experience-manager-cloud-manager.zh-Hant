---
title: 程式設定
description: 入職後，業務所有者需要對程式進行一些初始設定。
exl-id: 795c7112-d564-4fbf-96a1-152a6c286bf2
source-git-commit: 6572c16aea2c5d2d1032ca5b0f5d75ade65c3a19
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 0%

---


# 程式設定 {#program-setup}

入職後，業務所有者完成程式的初始設定，包括設定程式說明和定義用於效能測試的關鍵績效指標(KPI)。

## 程式設定 [!UICONTROL Cloud Manager] {#program-setup-cloud-manager}

按照以下步驟設定程式並定義KPI。

1. 登錄到Cloud Manager(位於 [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com) 並選擇相應的組織。

1. 按一下 **安裝程式** 啟動設定進程。

   ![設定程式](/help/assets/set-up-program/setup1.png)

1. 在 **安裝程式** 對話框可以在三個標籤中輸入程式資訊。

   * **一般**
   * **KPI**
   * **設定**

1. 在 **常規** 頁籤，添加程式說明，或者通過按一下 **更改照片**。

   ![常規頁籤](/help/assets/Setup_Program-General.png)

1. 在 **KPI** 頁籤。 在此示例中，為 **AEM Sites** 和 **AEM Assets**。 您將能夠指定已許可的產品的KPI。

   * 請參閱一節 [關鍵績效指標](#kpis) 有關如何在雲管理器中衡量KPI的詳細資訊。

   ![定義KPI](/help/assets/Setup_Program-KPIs.png)

1. 在 **設定** 頁籤，如果為程式啟用了自動縮放，則可以為環境定義按需縮放選項。

   * 自動縮放僅適用於生產環境，可能不適用於所有客戶計畫。

   ![設定選項](/help/assets/Setup_Program-Provisioning.png)

1. 按一下 **保存** 的子菜單。

將建立您的程式。 在程式準備使用之前，配置資源可能需要幾分鐘。

## 編輯程式 {#editing-program}

可以在程式設定後編輯它們。 按照以下步驟編輯程式。

1. 登錄到Cloud Manager(位於 [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com) 並選擇相應的組織。

1. 從Cloud Manager主螢幕導航到程式。

1. 按一下 **編輯程式** 從 **概述** 的子菜單。

   ![編輯程式選項](/help/assets/set-up-program/edit-program1.png)

1. 的 **編輯程式** 對話框，允許您更新程式。 請參閱一節 [使用雲管理器的程式設定](#program-setup-cloud-manager) 的子菜單。

   ![編輯程式對話框](/help/assets/set-up-program/edit-program-general.png)

1. 按一下 **更新** 的子菜單。

請注意，這些更改會立即保存到Cloud Manager，但在下次管道運行之前不會反映在您的環境中。

如果尚未建立管道，請查看文檔 [配置生產管線](/help/using/production-pipelines.md) 和 [配置非生產管道。](/help/using/non-production-pipelines.md)

## 在程式之間切換 {#swithing-programs}

在處理程式時，您可以快速切換到其他程式，而不返回Cloud Manager概述頁。

使用操作欄可切換到其他程式、編輯當前程式或添加新程式。

![節目切換器](/help/assets/set-up-program/setup2.png)

## 關鍵績效指標 {#kpis}

站點KPI是在登台環境上運行的test上衡量的。 通常，這些KPI會按照登台環境的功能進行縮放。

例如，在生產環境中，預期平均每分鐘有1000個頁面視圖，並且在生產中有四個調度程式/發佈伺服器的用戶應將此視圖擴展到每分鐘250個頁面視圖。 這假定其登台環境僅包含單個調度程式/發佈伺服器對。

資產效能測試是通過在30分鐘的test期間反複上載資產並測量每個資產的處理時間以及各種系統級度量來完成的。

您的生產環境前面可能有一個內容交付網路(CDN)，如Akamai或CloudFront。 自 [!UICONTROL Cloud Manager] 直接針對轉移環境test,KPI應僅反映預期通過CDN的流量，即快取未命中。 通常，這將是總生產流量中相對較小的子集。

## 視頻概述 {#video}

>[!VIDEO](https://video.tv.adobe.com/v/26313/)
