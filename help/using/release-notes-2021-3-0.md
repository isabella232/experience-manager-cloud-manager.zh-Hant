---
title: 2021.3.0 版發行說明
description: 請詳閱本頁以取得Cloud Manager 2021.3.0版的資訊
feature: 發行資訊
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: 503d9b25855633737c49e3e278a3a76052ed84d1
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 5%

---

# 2021.3.0 版發行說明 {#release-notes-for}

以下章節概述[!UICONTROL Cloud Manager] 2021.3.0版的一般發行說明。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2021.3.0版的發行日期為2021年3月11日。
下一版預計於2021年4月8日發行。

## 新功能 {#whats-new}

* 推出新的程式碼品質工具[Dispatcher最佳化工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/custom-code-quality-rules.html?lang=en#dispatcher-optimization-tool-rules)，以驗證客戶Dispatcher設定。

* 使用者現在可以在導覽至統一殼層的「使用者設定檔」圖示（右上）後，選取&#x200B;**檢視Cloud Manager角色**&#x200B;選項，即可查看其Cloud Manager角色。

* 標籤&#x200B;**申請核准**&#x200B;已重新標示為&#x200B;**生產核准**，以更清楚明瞭。

* 在「生產管道」執行畫面中，**Version**&#x200B;標籤已重新標示為&#x200B;**Git Tag**。

* 當重要量度不符合定義的臨界值時，定義行為的標籤已重新標示，以反映其真實行為 — **取消立即**&#x200B;和&#x200B;**立即核准**。 如需詳細資訊，請參閱[設定管道設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html?lang=en#configuring-the-pipeline-settings-from-cloud-manager) 。

* 類別和方法取代清單已根據AEMCloud ServiceSDK的`2021.3.4997.20210303T022849Z-210225`版本更新。

## 錯誤修正 {#bug-fixes}

* 將包嵌入其他包時，未正確發現某些質量問題。

* 有時，如果使用者在啟動管道後立即離開管道執行頁面進行導覽，雖然實際上會開始執行，但會顯示錯誤訊息，指出動作失敗。
