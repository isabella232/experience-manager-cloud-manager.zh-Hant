---
title: 2019.6.0 版發行說明
seo-title: Cloud Manager AEM 2019.6.0發行說明
description: 請依照本頁取得Cloud Manager 2019.6.0版的相關資訊。
seo-description: 請依照本頁取得AEMCloud Manager 2019.6.0版的資訊。
feature: 發行資訊
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 9%

---

# 2019.6.0 版發行說明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2019.6.0版本新增了程式碼品質規則和新的產品更新精靈。 請依照下列章節瞭解詳細資訊。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2019.6.0版的發行日期為2019年6月20日。

## 新功能 {#whats-new}

* 「新產品更新」精靈可協助客戶成功執行AEM更新。 請參閱[產品更新精靈](overview-productupdate-wizard.md)以瞭解更多資訊。
* 檢查內容結構的程式碼品質規則。 如需詳細資訊，請參閱[自訂代碼品質規則](custom-code-quality-rules.md)。
* Git推播的最大大小已增加至1 GB。

## 錯誤修正 {#bug-fixes}

* 在某些情況下，由於先前出現故障，無法啟動管道。

## 已知問題 {#known-issues}

* 程式碼品質CSV下載並非一律會依嚴重性排序。
* 如果OSGi組態位於&#x200B;*config*&#x200B;資料夾下的巢狀資料夾中，*ConfigAndInstallShoudOnlyContainOsgiNodes*&#x200B;規則可能會報告誤報。