---
title: 2021.5.0 版發行說明
description: 請詳閱本頁，了解Cloud Manager 2020.5.0版的相關資訊
feature: 發行資訊
source-git-commit: 3f17f252d89a1753c9cb121461b048f619d28415
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 5%

---

# 2021.5.0 版發行說明 {#release-notes-for}

以下章節概述[!UICONTROL Cloud Manager] 2021.5.0版的一般發行說明。

>[!NOTE]
>請參閱[最新發行說明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/release-notes-cloud-manager/release-notes-cm-current.html?lang=en#getting-access) ，查看AEM as aCloud Service中Cloud Manager的最新發行說明。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2021.5.0版的發行日期為2021年5月6日。
下一版預計於2021年6月10日發行。

## 新功能 {#whats-new}

* PackageOverlaps質量規則現在會檢測在同一部署的包集中多次部署相同包的情況，即在多個嵌入位置中。

* 公用API中的存放庫端點現在包含Git URL。

* 在「編輯方案」工作流程中，使用者只能設定非小數KPI值。

* 現在已解決將程式碼推送至AdobeGit時發生的間歇性故障。

* 已重新整理「編輯程式」體驗。

## 錯誤修正 {#bug-fixes}

* 管道變數API不會移除「已刪除」變數，而只會將其標示為狀態為「已刪除」。

* 某些代碼氣味類型的質量問題錯誤地影響了可靠性等級。

* 當午夜至凌晨1:00之間開始執行管道時，Cloud Manager產生的工件版本不一定會大於前一天建立的版本。

* 某些Adobe Managed Services(AMS)客戶無法使用Cloud Manager API在Adobe I/O開發人員控制台中建立新專案。
