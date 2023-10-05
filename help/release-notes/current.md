---
title: 2023.10.0 版發行說明
description: 以下是 Cloud Manager 2023.10.0 版的發行說明。
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: a5a304541409bc1775090eef2a669e1e0bcf005e
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 58%

---


# Cloud Manager 2023.10.0 版的發行說明 {#release-notes}

本頁記錄 [!UICONTROL Cloud Manager] 2023.10.0 版的發行說明。

>[!NOTE]
>
>如需 AEM as a Cloud Service 中 Cloud Manager 的最新發行說明，請參閱 [AEM as a Cloud Service 中 Cloud Manage 的最新發行說明。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2023.10.0 版的發行日期為 2023 年 10 月 5 日。下一個版本計畫於 2023 年 11 月 2 日發行。

## 新增功能 {#what-is-new}

* 此 **部署管理員** 角色可以 [設定在執行非生產管道時會失效或從AEM Dispatcher快取中排清的一組內容路徑。](/help/using/non-production-pipelines.md)
   * 在部署任何內容套件後，這些快取操作將以部署管道步驟的一部分來執行。
   * 這些設定會使用標準的 AEM Dispatcher 行為。
* 在2023年10月發行的Cloud Manager中，Java版本正在透過分階段推出進行更新。
   * Java版本正在更新以OracleJDK 8u371和OracleJDK 11.0.20。
   * [請參閱OpenJDK公告](https://openjdk.org/groups/vulnerability/advisories/) 瞭解這些JDK更新中的安全性和錯誤修正的詳細資訊。
