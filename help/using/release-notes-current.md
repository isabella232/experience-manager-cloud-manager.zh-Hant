---
title: 2021.8.0 版發行說明
description: 請詳閱本頁以取得Cloud Manager 2021.8.0版的資訊
feature: 發行資訊
source-git-commit: 510c523423a8d7cf9ad4c5ba2af11ff12df2b1cc
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 8%

---

# 2021.8.0 版發行說明 {#release-notes-for}

以下章節概述[!UICONTROL Cloud Manager] 2021.8.0版的一般發行說明。

>[!NOTE]
>請參閱[最新發行說明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/release-notes-cloud-manager/release-notes-cm-current.html?lang=en#getting-access) ，查看AEM as aCloud Service中Cloud Manager的最新發行說明。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2021.8.0版的發行日期為2021年8月12日。
下一版預計於2021年9月9日發行。

## 新增功能 {#whats-new}

* 自助服務功能可讓使用者透過Cloud Manager UI建立和管理多個存放庫。

* SonarQube不必要地閱讀git歷史資料。 在大型程式碼基底中，這可能會導致不必要的組建效能損失。

* 現在有API可用來使每個管道的Maven相依性快取失效。

* Cloud Manager使用的AEM專案原型版本已更新為28版。

## 錯誤修正 {#bug-fixes}

* 有時，當管道因某些原因觸發兩次時，會導致其中一個執行失敗，並出現&#x200B;*無法更新管道執行狀態*&#x200B;錯誤。
