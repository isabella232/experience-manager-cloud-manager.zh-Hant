---
title: 2018.7.0版發行說明
seo-title: 2018.7.0版發行說明
description: 'null'
seo-description: 請依照此頁面取得Cloud Manager版本2018.7.0的資訊。
uuid: d7b49e32-01dc-48ce-b744-e6 a806 fbdd8 a
contentOwner: jsyal
topic-tags: 版本注意事項
products: SG_ PERIENCENCENAGER/CLUDManager
discoiquuid: b64fb9ab-27ed-4f33-adc8-d73 d34094 f1 b
translation-type: tm+mt
source-git-commit: 1dfb065c09569f811e5a006d3d74825d3bd7cc8d

---


# 2018.7.0版發行說明 {#release-notes-for}

下節概述 [!UICONTROL Cloud Manager] 2018.7.0提供 *自動調整* 功能的版本。

**自動調整** 是透過在生產環境上水平縮放 `Dispatcher/Publish` 區段來啓用，以支援負載、體積、存取和其他定義的監控度量突然增加。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2018.7.0版的發行日期為2018年月10日。

## 新功能 {#what-s-new}

* **Provisioning** - [!UICONTROL Cloud Manager] 現在可以透過Dispatcher/Publish區段水平縮放，自動調整客戶計劃的生產環境。UI中的新功能是Program Setup中的「Provisioning」(布建)區段，如果客戶計劃啓用自動調整功能，則會顯示此區段。請參閱 [設定您的方案](setting-up-program.md) 以瞭解更多資訊。

* **環境** -現在可以查看「生產」和「舞台」環境的詳細檢視，以及與每個環境相關聯的大小、儲存空間、地區和狀態的詳細檢視。請參閱 [管理您的環境](manage-your-environment.md) 以瞭解更多資訊。

* **程式碼品質分析** -新規則以識別錯誤的API使用情況。請參閱 [自訂代碼品質規則](custom-code-quality-rules.md) 以瞭解更多資訊。

* **效能測試** -在檢視效能測試結果時，CPU使用率、磁碟I/等候時間、頁面錯誤率、磁碟頻寬使用率、網路頻寬使用率、峰值頁面回應時間和第95個百分點的頁面回應時間都有圖表。請參閱 [「瞭解測試結果](understand-your-test-results.md) 頁面上的效能測試*」一節。

* **效能測試** -檢視效能測試結果時，可下載頁面錯誤和緩慢請求的清單。請參閱 [「瞭解測試結果](understand-your-test-results.md) 頁面上的效能測試*」一節。

## 錯誤修正 {#bug-fixes}

* 在某些情況下，內部系統同步不適當，導致資料檢視不一致。
* 在某些情況下，手動管線觸發並未自動選取，導致表單驗證問題。
* 特定的客戶組建指令碼可能會根據外掛程式不相容而在組建步驟中造成失敗。

## 已知問題 {#known-issues}

* 雖然客戶可以選擇提交觸發觸發，但實際上不會根據新的通知開始。
* [!UICONTROL Experience Cloud] 通知資訊看板無法一致地載入通知。但是，通知會顯示在其中， [!UICONTROL Experience Cloud] 如果設定，仍會透過電子郵件傳送。

