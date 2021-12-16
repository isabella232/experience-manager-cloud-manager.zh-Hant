---
title: 2021.3.0 版發行說明
description: 請詳閱本頁以取得Cloud Manager 2021.3.0版的資訊
feature: Release Information
source-git-commit: 09dd8fe608d95cd9dbc95129cf86b9693c2839b5
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 5%

---

# 2021.3.0 版發行說明 {#release-notes-for}

以下章節概述的一般發行說明 [!UICONTROL Cloud Manager] 版本2021.3.0。

## 發行日期 {#release-date}

的發行日期 [!UICONTROL Cloud Manager] 2021.3.0版是2021年3月11日。
下一版預計於2021年4月8日發行。

## 新增功能 {#whats-new}

* 新的程式碼品質工具 [Dispatcher最佳化工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/custom-code-quality-rules.html?lang=en#dispatcher-optimization-tool-rules) 已導入以驗證customer dispatcher設定。

* 使用者現在可以透過選取 **檢視Cloud Manager角色** 選項(在導覽至「統一殼層」的「使用者設定檔」圖示（右上）後)。

* 標籤 **申請批准** 已重新標籤為 **生產核准** 更清晰。

* 此 **版本** 標籤已重新標籤為 **Git標籤** 在「生產管道」執行畫面中。

* 當重要量度不符合定義的臨界值時，定義行為的標籤已重新標示，以反映其真實行為 —  **立即取消** 和 **立即核准**. 請參閱 [配置管道設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html?lang=en#configuring-the-pipeline-settings-from-cloud-manager) 以取得更多詳細資訊。

* 類別和方法取代清單已根據版本更新 `2021.3.4997.20210303T022849Z-210225` AEM Cloud Service SDK的ID服務。

## 錯誤修正 {#bug-fixes}

* 將包嵌入其他包時，未正確發現某些質量問題。

* 有時，如果使用者在啟動管道後立即離開管道執行頁面進行導覽，雖然實際上會開始執行，但會顯示錯誤訊息，指出動作失敗。
