---
title: 2023.11.0 版發行說明
description: 以下是 Cloud Manager 2023.11.0 版的發行說明。
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: c7803c75bcfcc967877808214704c5746015481d
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 31%

---


# Cloud Manager 2023.11.0 版的發行說明 {#release-notes}

本頁記錄 [!UICONTROL Cloud Manager] 2023.11.0 版的發行說明。

>[!NOTE]
>
>如需 AEM as a Cloud Service 中 Cloud Manager 的最新發行說明，請參閱 [AEM as a Cloud Service 中 Cloud Manage 的最新發行說明。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2023.11.0 版的發行日期為 2023 年 11 月 14 日。下一版本計畫於2023年12月7日發行。

## 新增功能 {#what-is-new}

* [管道執行詳細資訊頁面](/help/using/managing-pipelines.md#view-details) 現在會顯示管道執行中的所有步驟，其中尚未開始的步驟會呈現灰色。
* 在兩者上 **[活動](/help/using/managing-pipelines.md#activity)** 和 **[管道](/help/using/managing-pipelines.md#pipelines)** 頁面上，現在當按一下具有執行狀態的管道時，會顯示管道執行的摘要。
* 新 **持續時間** 區段已新增至 [管道詳細資訊頁面](/help/using/managing-pipelines.md#view-details) 這包括根據該計畫歷史趨勢的管道步驟平均持續時間。
* 在管道執行頁面上，完成的步驟現在顯示持續時間
* Cloud Manager [內容複製工具](/help/using/content-copy.md) 可讓使用者隨選從其AMS代管的AEM 6.x生產環境複製可變內容至較低環境，以用於測試用途。

## 早期採用計劃 {#early-adoption}

成為我們早期採用計畫的一部分，並有機會測試一些即將推出的功能

### 自備GitHub {#byo-github}

如果您使用GitHub管理存放庫， [您現在可以透過Cloud Manager直接在GitHub存放庫中驗證程式碼。](/help/managing-code/byo-github.md) 此整合免除了與Adobe存放庫一致同步程式碼的需求，並可讓您在合併提取請求至主要分支之前先驗證提取請求。

如果您有興趣測試這項新功能並分享您的回饋意見，請傳送電子郵件至 `Grp-CloudManager_BYOG@adobe.com` 來自與Adobe ID相關聯的電子郵件地址。

### 自訂權限 {#custom-permissions}

[Cloud Manager 自訂權限](/help/using/custom-permissions.md)允許您以可設定的權限建立新的自訂權限設定檔，以限制 Cloud Manager 使用者對程式、管道和環境的存取。

如果您有興趣測試這項新功能並分享您的回饋意見，請傳送電子郵件至 `Grp-CloudManager_ams_custompermissions@adobe.com` 來自與Adobe ID相關聯的電子郵件地址。
