---
title: 2024.1.0 版發行說明
description: 以下是 Cloud Manager 2024.1.0 版的發行說明。
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: b5907179d3de329e8b86546bb8aa99608a5b351a
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 84%

---


# Cloud Manager 2024.1.0 版的發行說明 {#release-notes}

本頁記錄 [!UICONTROL Cloud Manager] 2024.1.0 版的發行說明。

>[!NOTE]
>
>如需 AEM as a Cloud Service 中 Cloud Manager 的最新發行說明，請參閱 [AEM as a Cloud Service 中 Cloud Manage 的最新發行說明。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2024.1.0 版的發行日期為 2024 年 1 月 17 日。下一版計畫於 2024 年 2 月 16 日發行。

## 早期採用計劃 {#early-adoption}

參加我們的早期採用計劃，即有機會測試一些即將推出的功能。

### 帶著您自己的 GitHub {#byo-github}

如果您使用 GitHub 來管理您的存放庫，[現在您可以透過 Cloud Manager 直接在 GitHub 存放庫中驗證程式碼。](/help/managing-code/byo-github.md) 此整合免除了與Adobe存放庫一致同步程式碼的需求，並可讓您在合併提取請求至主要分支之前先驗證提取請求。 此功能是公共GitHub的專屬功能。 不支援自行託管GitHub。

如果您有興趣測試此新功能並分享您的意見反饋，請使用和您的 Adobe ID 相關聯的電子郵件傳送一封電子郵件至 `Grp-CloudManager_BYOG@adobe.com`。

## 錯誤修正 {#bug-fixes}

* 修正了某些極端情況下的錯誤，這些情況下由於測試應用程式解釋資料的方式而導致下載失敗，從而導致總錯誤百分比無法通過測試。
* 當建置步驟由於 `BUILD_MAVEN_TRANSFER_ARTIFACT_ERROR` 而以 `FAILED` 狀態完成時，現在可以正確地將其描述為由於與目標分支的合併衝突而導致的錯誤。
