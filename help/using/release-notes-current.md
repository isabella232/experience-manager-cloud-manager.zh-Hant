---
title: 2019.6.0版發行說明
seo-title: 2019.6.0版AEM Cloud Manager發行說明
description: 請依照此頁面取得Cloud Manager發行2019.6.0的資訊。
seo-description: 請依照此頁面取得AEM Cloud Manager發行2019.6.0的資訊。
translation-type: tm+mt
source-git-commit: 7373f674b9804c83fad0871a74ef85280ea24962

---

# Release Notes for 2019.6.0 {#release-notes-for}

[!UICONTROL Cloud Manager] 2019.6.0版本新增了程式碼品質規則和新的產品更新精靈。請遵循下列章節以瞭解詳細資訊。

## Release Date {#release-date}

[!UICONTROL Cloud Manager] 2019.6.0版的發行日期為2019年月20日。

## 新功能 {#whats-new}

* 新產品更新精靈可協助客戶成功執行AEM更新。Refer to [Product Update Wizard](overview-productupdate-wizard.md) to learn more.
* 檢查內容結構的程式碼品質規則。Refer to [Custom Code Quality Rules](custom-code-quality-rules.md) for more information.
* Git推播的大小上限已提高為GB。

## Bug Fixes {#bug-fixes}

* 在某些情況下，由於發生先前失敗，管線無法啓動。

## 已知問題 {#known-issues}

* 不一定會根據嚴重性排序程式碼品質CSV下載。
* *如果* OSGi組態放置在 *config* 資料夾下的巢狀資料夾中，則ConfigAndInstallshordonlycontrough OsyDays規則可能會報告錯誤的位置。
