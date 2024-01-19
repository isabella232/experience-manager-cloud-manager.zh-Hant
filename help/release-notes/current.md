---
title: 2024.1.0 版發行說明
description: 以下是 Cloud Manager 2024.1.0 版的發行說明。
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: b235e398b42e9da3dd2efacdc0ef38b6803bd213
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 77%

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

如果您使用 GitHub 來管理您的存放庫，[現在您可以透過 Cloud Manager 直接在 GitHub 存放庫中驗證程式碼。](/help/managing-code/byo-github.md)這種整合消除了始終將程式碼與 Adobe 存放庫保持同步的需要，並允許您先確認提取要求再將其合併到主要分支。

如果您有興趣測試此新功能並分享您的意見反饋，請使用和您的 Adobe ID 相關聯的電子郵件傳送一封電子郵件至 `Grp-CloudManager_BYOG@adobe.com`。

## 錯誤修正 {#bug-fixes}

* 已針對某些轉角案例更正錯誤，這類案例中，由於測試應用程式如何解讀資料，而導致下載失敗，導致總錯誤百分比無法通過測試。
* 當建置步驟以狀態完成時 `FAILED` 由於 `BUILD_MAVEN_TRANSFER_ARTIFACT_ERROR`，現在會正確描述為由於與目的地分支合併衝突而導致的錯誤。
