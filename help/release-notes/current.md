---
title: 2024.2.0 版發行說明
description: 以下是 Cloud Manager 2024.2.0 版的發行說明。
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: 524471a87217c15dae96c3e6aee57426b43dcccb
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 68%

---


# Cloud Manager 2024.2.0 版的發行說明 {#release-notes}

本頁記錄 [!UICONTROL Cloud Manager] 2024.2.0 版的發行說明。

>[!NOTE]
>
>如需 AEM as a Cloud Service 中 Cloud Manager 的最新發行說明，請參閱 [AEM as a Cloud Service 中 Cloud Manage 的最新發行說明。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2024.2.0 版的發行日期為 2024 年 2 月 16 日。下一個版本計畫於 2024 年 3 月 16 日發行。

## 新增功能 {#what-is-new}

* 做為的一部分 [部署，](/help/using/code-deployment.md) Dispatcher快取已在 **附加Dispatcher** 步驟。 為了讓您在將每個節點附加到應用程式負載平衡器之前測試其上的變更，在部署程式碼到特定發佈者後，您現在可以在將該Dispatcher附加到負載平衡器之前直接從關聯的Dispatcher測試變更。
* [組建環境](/help/getting-started/build-environment.md) 已更新至Maven 3.9.4版和JDK jdk-11.0.22版和jdk1.8.0_401版。

## 早期採用計劃 {#early-adoption}

參加我們的早期採用計劃，即有機會測試一些即將推出的功能。

### 帶著您自己的 GitHub {#byo-github}

如果您使用 GitHub 來管理您的存放庫，[現在您可以透過 Cloud Manager 直接在 GitHub 存放庫中驗證程式碼。](/help/managing-code/byo-github.md)透過此一整合，便不再需要持續與 Adobe 存放庫進行程式碼同步化，並讓您可以先確認提取要求再將其合併到主要分支。這是公開 GitHub 的專屬功能。不支援自行託管的 GitHub。

如果您有興趣測試這項新功能並分享意見回饋，請使用與您的 Adobe ID 相關聯的電子郵件傳送一封郵件至 `Grp-CloudManager_BYOG@adobe.com`。

## 錯誤修正 {#bug-fixes}

* 組建容器的JDK已更新至可解決的版本 [JDK-8313765。](https://bugs.openjdk.org/browse/JDK-8313765)
