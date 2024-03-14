---
title: 2024.3.0 版發行說明
description: 以下是 Cloud Manager 2024.3.0 版的發行說明。
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: 22730ba281f7c1c4720158a3a813c56b815a0af1
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 76%

---


# Cloud Manager 2024.3.0 版的發行說明 {#release-notes}

本頁記錄 [!UICONTROL Cloud Manager] 2024.3.0 版的發行說明。

>[!NOTE]
>
>如需 AEM as a Cloud Service 中 Cloud Manager 的最新發行說明，請參閱 [AEM as a Cloud Service 中 Cloud Manage 的最新發行說明。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2024.3.0 版的發行日期為 2024 年 3 月 14 日。下一版本計畫於 2024 年 4 月 11 日發行。

## 新增功能 {#what-is-new}

* Cloud Manager UI中現在會顯示包括綠色伺服器的IP/DNS (FQDN)資訊的細節。

## 早期採用計劃 {#early-adoption}

參加我們的早期採用計劃，即有機會測試一些即將推出的功能。

### 帶著您自己的 GitHub {#byo-github}

如果您使用 GitHub 來管理您的存放庫，[現在您可以透過 Cloud Manager 直接在 GitHub 存放庫中驗證程式碼。](/help/managing-code/byo-github.md)透過此一整合，便不再需要持續與 Adobe 存放庫進行程式碼同步化，並讓您可以先確認提取要求再將其合併到主要分支。這是公開 GitHub 的專屬功能。不支援自行託管的 GitHub。

如果您有興趣測試這項新功能並分享意見回饋，請使用與您的 Adobe ID 相關聯的電子郵件傳送一封郵件至 `Grp-CloudManager_BYOG@adobe.com`。

## 錯誤修正 {#bug-fixes}

* 已修正當錯誤率量度失敗時，效能測試步驟中未產生適當記錄檔時的錯誤。
* 效能測試服務內用於偵測網站(404)上無頁面的邏輯，現在可確保更順暢、不間斷的部署。
