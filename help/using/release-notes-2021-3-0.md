---
title: 2021.3.0 版發行說明
description: 按照本頁獲取Cloud Manager 2021.3.0版的資訊
feature: Release Information
exl-id: e05b22fe-f071-4b69-9db1-e3d7ee4cfbcc
source-git-commit: 71d44c7e3673ca62fcd2203ecc0bc4ed9fa22002
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 5%

---

# 2021.3.0 版發行說明 {#release-notes-for}

以下部分概述了有關 [!UICONTROL Cloud Manager] 2021.3.0版。

## 發行日期 {#release-date}

發放日期 [!UICONTROL Cloud Manager] 版本2021.3.0為2021年3月11日。
下一版計畫於2021年4月08日發行。

## 新增功能 {#whats-new}

* 一種新的代碼質量工具 [Dispatcher優化工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/custom-code-quality-rules.html?lang=en#dispatcher-optimization-tool-rules) 已引入以驗證客戶調度程式配置。

* 用戶現在可以通過選擇 **查看雲管理器角色** 選項。

* 標籤 **申請審批** 被重新安排 **生產審批** 更清晰。

* 的 **版本** 標籤已重新標籤為 **Git標籤** 在「生產管道」執行螢幕中。

* 當重要度量不滿足定義的閾值時定義行為的標籤已重新標籤以反映其真實行為 —  **立即取消** 和 **立即批准**。 請參閱文檔 [配置生產管線](configuring-production-pipelines.md) 的子菜單。

* 類和方法棄用清單已根據版本進行更新 `2021.3.4997.20210303T022849Z-210225` AEM Cloud Service軟體開發工具包。

## 錯誤修正 {#bug-fixes}

* 當將包嵌入到其他包中時，未正確發現某些質量問題。

* 有時，如果用戶在啟動管道後立即從管道執行頁面導航出去，則會顯示一條錯誤消息，指出操作失敗，儘管實際上執行會開始。
