---
title: 2019.9.0發行說明
seo-title: AEM Cloud manager 2019.9.0版本注意事項
description: 請依照本頁取得Cloud Manager 2019.9.0版的相關資訊。
seo-description: 請依照本頁取得AEM Cloud Manager 2019.9.0版的相關資訊。
translation-type: tm+mt
source-git-commit: 26014cfabfee6226033ba2fc1167d8f5509e17c6

---

# 2019.9.0發行說明 {#release-notes-for}

2019.9.0 [!UICONTROL Cloud Manager] 版本會更新安全性測試標準、新增可下載的監控圖表，並修正客戶報告的可用性問題。

## 發行日期 {#release-date}

2019.9.0版 [!UICONTROL Cloud Manager] 的發行日期為2019年9月12日。

## 新功能 {#whats-new}

* Sling Referrer Filter Health check的分類已從Critical變更為Importent。
* HTML Library Manager config運行狀況檢查的分類已從「Critical（關鍵）」更改為「Mignent（重要）」。
* Monitoring graphs can now be downloaded. Refer to Monitor your Environments for more details.[](monitor-your-environments.md)
* If a program does not have a production AEM environment, clicking on the program card from the landing page will navigate to the Cloud Manager overview page, not produce an error dialog.
* The Pipeline Settings Card on the Overview page has been retitled to Production Pipeline Settings.************
* The Important Failure Behavior radio buttons have been removed from code-quality only pipelines.
* The Activity page now displays the name of the pipeline for each execution.****
* The execution page now displays the name of the pipeline.
* The Code Quality summary dialog now shows a description for each rating.

## Bug Fixes {#bug-fixes}

* Some users could not view an execution details when it was waiting for approval.
* On Overview page, the right margin was not consistent.****
* The build container could run out of memory in large projects.
* Under certain circumstances, the BannedPaths OakPAL rule did not identify installed content under /libs.
* When a quality gate was rejected, the dialog heading still showed Partially Passed.**

## 已知問題 {#known-issues}

* Downloading of monitoring graphs is not available in Safari.
