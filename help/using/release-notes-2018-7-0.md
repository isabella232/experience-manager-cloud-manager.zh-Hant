---
title: 2018.7.0 版發行說明
seo-title: 2018.7.0 版發行說明
description: 了解Cloud Manager 2018.7.0版
seo-description: 請詳閱本頁以取得Cloud Manager 2019.7.0版的資訊。
uuid: d7b49e32-01dc-48ce-b744-e6a806fbdd8a
contentOwner: jsyal
topic-tags: release-notes
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
discoiquuid: b64bf9ab-27ed-4f33-adc8-d73d34094f1b
feature: 發行資訊
exl-id: fc0214b4-d138-470a-9b04-191224927f7b
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 12%

---

# 2018.7.0 版發行說明 {#release-notes-for}

以下章節概述了提供&#x200B;*autoscaling*&#x200B;功能的[!UICONTROL Cloud Manager] 2018.7.0版本。

**自動擴充功能是透過生產環境中 區段的橫向擴充功能來啟用，用於支援突然增加的負載、磁碟區、存取和其他已定義的監控量度。**`Dispatcher/Publish`

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2018.7.0版的發行日期為2018年9月10日。

## 新功能 {#what-s-new}

* **布建**  -  [!UICONTROL Cloud Manager] 現在能透過水準縮放Dispatcher/Publish區段，自動縮放客戶程式上的生產環境。UI中的新功能是「方案設定」中的「布建」區段，如果客戶方案已啟用自動縮放，該區段會顯示。 請參閱[設定您的程式](setting-up-program.md)以了解更多資訊。

* **環境**  — 您現在可以檢視生產和預備環境的詳細檢視，以及與每個環境相關聯的節點的大小、儲存、地區和狀態。請參閱[管理環境](manage-your-environment.md)以了解更多資訊。

* **程式碼品質分析**  — 識別錯誤API使用方式的新規則。請參閱[自訂程式碼品質規則](custom-code-quality-rules.md)以深入了解。

* **效能測試**  — 在查看效能測試結果時，可使用CPU利用率、磁碟I/O等待時間、頁錯誤率、磁碟頻寬利用率、網路頻寬利用率、峰值頁面響應時間和第95個百分位數頁面響應時間的圖表。請參閱[了解測試結果](understand-your-test-results.md)頁面上的&#x200B;*效能測試*&#x200B;一節。

* **效能測試**  — 檢視效能測試結果時，可下載頁面錯誤和慢速請求的清單。請參閱[了解測試結果](understand-your-test-results.md)頁面上的&#x200B;*效能測試*&#x200B;一節。

## 錯誤修正 {#bug-fixes}

* 在某些情況下，內部系統同步失敗，導致資料視圖不一致。
* 在某些情況下，手動管道觸發器未自動選取，導致表單驗證問題。
* 根據外掛程式不相容，特定客戶建置指令碼可能會在建立步驟期間造成失敗。

## 已知問題 {#known-issues}

* 雖然客戶可以選擇提交觸發器，但管道實際上可能不會基於新提交而啟動。
* [!UICONTROL Experience Cloud]通知側欄可能無法一致地載入通知。 不過，通知會顯示在[!UICONTROL Experience Cloud]中，如果已設定，仍會透過電子郵件傳送。
