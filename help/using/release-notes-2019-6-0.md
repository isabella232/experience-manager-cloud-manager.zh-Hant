---
title: 2019.6.0 版發行說明
seo-title: AEM Cloud Manager 2019.6.0版發行說明
description: 請詳閱本頁以取得Cloud Manager 2019.6.0版的資訊。
seo-description: 請詳閱本頁以取得AEM Cloud Manager 2019.6.0版的資訊。
feature: 發行資訊
exl-id: 5a87f191-8203-4cb9-a810-247aece41605
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 9%

---

# 2019.6.0 版發行說明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2019.6.0版新增了新的程式碼品質規則和新的產品更新精靈。 如需詳細資訊，請參閱以下各節。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2019.6.0版的發行日期為2019年6月20日。

## 新功能 {#whats-new}

* 新產品更新精靈可協助客戶成功執行AEM更新。 請參閱[產品更新精靈](overview-productupdate-wizard.md)以深入了解。
* 檢查內容結構的程式碼品質規則。 如需詳細資訊，請參閱[自訂程式碼品質規則](custom-code-quality-rules.md)。
* Git推播的最大大小已增加至1 GB。

## 錯誤修正 {#bug-fixes}

* 在某些情況下，由於以前的故障，無法啟動管道。

## 已知問題 {#known-issues}

* 程式碼品質CSV下載並非一律會根據嚴重性排序。
* 如果OSGi設定放在&#x200B;*config*&#x200B;資料夾下的巢狀資料夾中，*ConfigAndInstallShouldOnlyContainOsgiNodes*&#x200B;規則可能會回報誤判。
