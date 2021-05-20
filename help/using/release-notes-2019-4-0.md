---
title: 2019.4.0 版發行說明
seo-title: AEM Cloud Manager 2019.4.0版發行說明
description: 請詳閱本頁以取得Cloud Manager 2019.4.0版的資訊。
seo-description: 請詳閱本頁，以取得AEM Cloud Manager 2019.4.0版的資訊。
feature: 發行資訊
exl-id: 8ca6386c-5de9-48b8-9034-466d4913d5a9
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 7%

---

# 2019.4.0 版發行說明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2019.4.0版不包含重大功能變更。 如需詳細資訊，請參閱以下各節。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2019.4.0版的發行日期為2019年4月18日。

## 新功能 {#whats-new}

* Cloud Manager UI現在提供英文、法文、德文和日文版。
* 部署步驟現在包含當前正在運行的進程，即當備份運行時，正在安裝程式包，並且正在重新配置負載平衡器

## 錯誤修正 {#bug-fixes}

* 用於Dispatcher變更的部署方法已經過改良，可處理其他使用案例。
* 「環境」頁面未正確顯示某些執行個體大小類型。
* 程式碼品質規則CQBP-84相依性會為內嵌Adobe程式庫（例如WCM核心元件和資產共用公域）產生誤判。
* 當詳細資訊無法使用時，代碼掃描步驟的詳細資訊按鈕已啟用。
* 為每分鐘頁面檢視次數指定無效值時，KPI的下界錯誤。
* 非生產管道上的部署類別資本化不正確。
* 當Git存放庫未正確設定時，**概述**&#x200B;頁面上的動作卡呼叫有錯誤的文字。

## 已知問題 {#known-issues}

* SLA值可能會不正確四捨五入。
