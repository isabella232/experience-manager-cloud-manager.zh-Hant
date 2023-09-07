---
title: 2023.9.0 版發行說明
description: 以下是 Cloud Manager 2023.9.0 版的發行說明。
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: 74381d5d154f7c61135a990d2806fa9e39be7690
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 54%

---


# Cloud Manager 2023.9.0 版的發行說明 {#release-notes}

本頁記錄 [!UICONTROL Cloud Manager] 2023.9.0 版的發行說明。

>[!NOTE]
>
>如需 AEM as a Cloud Service 中 Cloud Manager 的最新發行說明，請參閱 [AEM as a Cloud Service 中 Cloud Manage 的最新發行說明。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2023.9.0 版的發行日期為 2023 年 9 月 7 日。下一版本計畫於 2023 年 10 月 5 日發行。

## 新增功能 {#what-is-new}

此版本包含錯誤修正。

## 錯誤修正 {#bug-fixes}

* 刪除程式時，也會刪除任何相關聯且正在執行的管道，以確保管道不會錯誤指定為失敗狀態。
* 有時，當管道執行的所有步驟都是「已完成」時，管道的狀態會視為「執行中」，使其看起來像是處於卡住狀態。 它現在會視為「完成」。
* 對於使用計畫碼產生器原型產生的存放庫分支，CI/CD管道會失敗。
