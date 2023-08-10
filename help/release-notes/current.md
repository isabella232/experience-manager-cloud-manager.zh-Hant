---
title: 2023.8.0 版發行說明
description: 以下是 Cloud Manager 2023.8.0 版的發行說明。
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: f930f12b5f50dd96a1677ff7a56cf0e92a400556
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 39%

---


# Cloud Manager 2023.8.0 版的發行說明 {#release-notes}

本頁記錄 [!UICONTROL Cloud Manager] 2023.8.0 版的發行說明。

>[!NOTE]
>
>如需 AEM as a Cloud Service 中 Cloud Manager 的最新發行說明，請參閱 [AEM as a Cloud Service 中 Cloud Manage 的最新發行說明。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2023.8.0 版的發行日期為 2023 年 8 月 10 日。下一個版本計畫於 2023 年 7 月 9 日發行。

## 新增功能 {#what-is-new}

* 已進行增強功能，以改善Cloud Manager UI中錯誤訊息的可理解性和顯示性。

## 錯誤修正 {#bug-fixes}

* 不常見的情況 [內容複製](/help/using/content-copy.md) 處理卡住的問題已解決。
* 已解決未使用New Relic One之客戶的暫時測試問題。
* [自訂程式碼品質規則](/help/using/custom-code-quality-rules.md) `SupportedRunmode` 和 `ImmutableMutableMixedPackage` 已從SonarQube移除，因為它們僅適用於AEMas a Cloud Service。
* 使用者不會再遇到似乎處於執行狀態的卡住管道。
* 此 **環境** 功能表現在會在觸發 **[複製內容](/help/using/content-copy.md)** 強制回應視窗。
* [管道重新執行](/help/using/code-deployment.md#reexecute-deployment) 如果先前執行沒有 `commitId` 在建置階段狀態上設定。
* 現在，當使用者按一下中的管道時，對於罕見錯誤，會顯示更易於理解的訊息 **活動** 或 **管道** 畫面。
