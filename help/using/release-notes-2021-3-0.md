---
title: 2021.3.0 版發行說明
description: 請依照本頁取得Cloud Manager 2021.3.0版的相關資訊
feature: 發行資訊
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
translation-type: tm+mt
source-git-commit: 13a918f69185c684ca69b812df7eb5c2bd43e064
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 5%

---

# 2021.3.0 版發行說明 {#release-notes-for}

下節概述[!UICONTROL Cloud Manager] 2021.3.0版的一般發行說明。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2021.3.0版的發行日期為2021年3月11日。
下一版預計於2021年4月08日推出。

## 新功能 {#whats-new}

* 引入了新的代碼質量工具[Dispatcher Optimization Tool](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/custom-code-quality-rules.html?lang=en#dispatcher-optimization-tool-rules)來驗證客戶分發程式配置。

* 現在，在導覽至Unified Shell的「用戶配置檔案」表徵圖（右上角）後，用戶可以選擇「查看雲管理員角色」****&#x200B;選項，以查看其Cloud Manager角色。

* **申請批准**&#x200B;標籤已重新標籤至&#x200B;**生產批准**，以更清楚明瞭。

* **版本**&#x200B;標籤已重新標籤至「生產管線」執行畫面中的&#x200B;**Git Tag**。

* 當重要量度不符合定義的臨界值時，定義行為的標籤已重新標籤，以反映其真實行為- **取消立即**&#x200B;和&#x200B;**批准立即**。 有關詳細資訊，請參閱[配置管線設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html?lang=en#configuring-the-pipeline-settings-from-cloud-manager)。

* 類別和方法取代清單已根據Cloud ServiceSDK的`2021.3.4997.20210303T022849Z-210225`版AEM本更新。

## 錯誤修正 {#bug-fixes}

* 在將包嵌入其他包時，未正確發現某些質量問題。

* 有時，如果用戶在啟動管線後立即導航離開管線執行頁面，則會顯示一條錯誤消息，指出操作失敗，儘管實際上執行開始。
