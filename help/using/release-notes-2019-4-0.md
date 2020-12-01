---
title: 2019.4.0 版發行說明
seo-title: AEM Cloud Manager 2019.4.0版本注意事項
description: 請依照本頁取得Cloud Manager 2019.4.0版的相關資訊。
seo-description: 請依照本頁取得AEM Cloud Manager 2019.4.0版的相關資訊。
translation-type: tm+mt
source-git-commit: b368c46c2a9f40d0c3867db6eb2a333bd71fe22a
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 6%

---


# 2019.4.0 版發行說明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2019.4.0版不包含重大功能變更。 請依照下列章節瞭解詳細資訊。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2019.4.0版的發行日期為2019年4月18日。

## 新功能 {#whats-new}

* Cloud Manager UI現在提供英文、法文、德文和日文版。
* 部署步驟現在包含當前正在運行的進程，即當備份運行時，正在安裝軟體包，並正在重新配置負載平衡器

## 錯誤修正 {#bug-fixes}

* 已改進用於Dispatcher更改的部署方法，以處理其他使用案例。
* 「環境」頁面上未正確顯示某些實例大小類型。
* 程式碼品質規則CQBP-84-dependencies會針對內嵌的Adobe程式庫（例如WCM核心元件和資產共用共用公域）產生誤報。
* 當詳細資訊無法使用時，程式碼掃描步驟的詳細資訊按鈕已啟用。
* 為每分鐘頁面檢視次數指定無效值時，KPI的下界值錯誤。
* 非生產管道上的部署類別資本不正確。
* 當git資料庫未正確設定時，**概述**&#x200B;頁面上對動作卡的呼叫有不正確的文字。

## 已知問題 {#known-issues}

* SLA值可能不正確四捨五入。
