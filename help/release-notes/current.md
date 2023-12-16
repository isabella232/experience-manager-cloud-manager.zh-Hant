---
title: 2023.12.0 版發行說明
description: 以下是 Cloud Manager 2023.12.0 版的發行說明。
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: 2ac254508e4015fea21c4fcd087703ac5fbeeec6
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 66%

---


# Cloud Manager 2023.12.0 版的發行說明 {#release-notes}

本頁記錄 [!UICONTROL Cloud Manager] 2023.12.0 版的發行說明。

>[!NOTE]
>
>如需 AEM as a Cloud Service 中 Cloud Manager 的最新發行說明，請參閱 [AEM as a Cloud Service 中 Cloud Manage 的最新發行說明。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## 發行日期 {#release-date}

的發行日期 [!UICONTROL Cloud Manager] 2023.12.0版將於2023年12月14日發行。 下一個版本計畫於 2024 年 1 月 18 日發行。

## 新增功能 {#what-is-new}

* [Cloud Manager 自訂權限](/help/using/custom-permissions.md)允許您以可設定的權限建立新的自訂權限設定檔，以限制 Cloud Manager 使用者對方案、管道和環境的存取。
* 將更新轉出到 [組建環境](/help/getting-started/build-environment.md) 曾經是 [宣佈並從10月版本的Cloud Manager開始](/help/release-notes/2023/2023-10-0.md) 已完成。
   * 新增對節點18的支援 [前端和完整棧疊管道。](/help/overview/ci-cd-pipelines.md)
   * Java 8次要版本已更新至 `jdk1.8.0_371`.
   * Java 11次要版本更新至 `jdk-11.0.20`.
   * Maven已更新至3.8.8版
      * Maven現在會停用所有不安全的專案 `http://*` 預設為映象。
      * [Adobe建議](/help/getting-started/build-environment.md#https-maven) 使用者更新其Maven存放庫以使用HTTPS而不是HTTP。
* 組建容器基礎影像已更新為Ubuntu 22.04。

## 早期採用計劃 {#early-adoption}

參加我們的早期採用計劃，即有機會測試一些即將推出的功能。

### 帶著您自己的 GitHub {#byo-github}

如果您使用 GitHub 來管理您的存放庫，[現在您可以透過 Cloud Manager 直接在 GitHub 存放庫中驗證程式碼。](/help/managing-code/byo-github.md)這種整合消除了始終將程式碼與 Adobe 存放庫保持同步的需要，並允許您先確認提取要求再將其合併到主要分支。

如果您有興趣測試此新功能並分享您的意見反饋，請使用和您的 Adobe ID 相關聯的電子郵件傳送一封電子郵件至 `Grp-CloudManager_BYOG@adobe.com`。
