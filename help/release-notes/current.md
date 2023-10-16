---
title: 2023.10.0 版發行說明
description: 以下是 Cloud Manager 2023.10.0 版的發行說明。
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: 851364e74864c28b3bcd9285dfbe06ddb530eb10
workflow-type: ht
source-wordcount: '226'
ht-degree: 100%

---


# Cloud Manager 2023.10.0 版的發行說明 {#release-notes}

本頁記錄 [!UICONTROL Cloud Manager] 2023.10.0 版的發行說明。

>[!NOTE]
>
>如需 AEM as a Cloud Service 中 Cloud Manager 的最新發行說明，請參閱 [AEM as a Cloud Service 中 Cloud Manage 的最新發行說明。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2023.10.0 版的發行日期為 2023 年 10 月 5 日。下一個版本計畫於 2023 年 11 月 2 日發行。

## 新增功能 {#what-is-new}

* **部署管理員**&#x200B;角色可以[設定在執行非生產管道時將失效或從 AEM Dispatcher 快取中排清的一連串內容路徑。](/help/using/non-production-pipelines.md)
   * 在部署任何內容套件後，這些快取操作將以部署管道步驟的一部分來執行。
   * 這些設定會使用標準的 AEM Dispatcher 行為。
* 隨著 Cloud Manager 2023 年 10 月版發行，Java 版本將分階段推出更新。
   * Java 8 和 11 以及 Maven 的次要版本已更新，將在未來 2 個月內分階段推出。新版本有多個安全性修正和錯誤修正。新版本為：
   * *Maven：3.8.8*
   * *Java 8 版：/usr/lib/jvm/jdk1.8.0_371*
   * *Java 11 版：/usr/lib/jvm/jdk-11.0.20*
   * [請參閱 OpenJDK 諮詢服務](https://openjdk.org/groups/vulnerability/advisories/)，了解這些 JDK 更新中的安全性和錯誤修正的詳細資訊。
