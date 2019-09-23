---
title: 2018.7.0發行說明
seo-title: 2018.7.0發行說明
description: 'null'
seo-description: 請依照本頁取得Cloud Manager 2018.7.0版的相關資訊。
uuid: d7b49e32-01dc-48ce-b744-e6a806fbdd8a
contentOwner: jsyal
topic-tags: 發行說明
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
discoiquuid: b64bf9ab-27ed-4f33-adc8-d73d34094f1b
translation-type: tm+mt
source-git-commit: b78c29520414726ad2bbf86e5b7f8e65710c7f75

---


# 2018.7.0發行說明 {#release-notes-for}

下節概述提供 [!UICONTROL Cloud Manager] 自動縮放功能的2018.7.0 *版本* 。

**自動縮放** ，可透過生產環境上區段的橫向縮放來 `Dispatcher/Publish` 啟用，以支援負載、容量、存取以及其他已定義的監控量度的突然增加。

## 發行日期 {#release-date}

2018.7.0版 [!UICONTROL Cloud Manager] 的發行日期為2018年9月10日。

## 新功能 {#what-s-new}

* **布建** -現 [!UICONTROL Cloud Manager] 在可以使用Dispatcher/Publish細分水準向外擴展，從而自動擴展客戶程式上的生產環境。 UI中的新功能是「方案設定」中的「布建」區段，如果在客戶方案上啟用自動縮放，則會顯示此區段。 請參閱設 [定您的方案](setting-up-program.md) ，瞭解更多。

* **環境** -現在可以詳細查看生產和階段環境以及與每個環境相關聯的節點的大小、儲存、區域和狀態。 請參閱「管 [理您的環境](manage-your-environment.md) 」以瞭解更多。

* **程式碼品質分析** -用以識別錯誤API使用情形的新規則。 請參閱自訂 [程式碼品質規則](custom-code-quality-rules.md) ，瞭解更多資訊。

* **效能測試** -在查看效能測試結果時，可以使用CPU利用率、磁碟I/O等待時間、頁錯誤率、磁碟頻寬利用率、網路頻寬利用率、峰值頁面響應時間和第95個百分位數頁面響應時間的圖表。 請參閱「瞭解測試結果」頁面上的「 [效能測試」](understand-your-test-results.md) *一節。

* **效能測試** -檢視效能測試結果時，可下載頁面錯誤和慢速請求清單。 請參閱「瞭解測試結果」頁面上的「 [效能測試」](understand-your-test-results.md) *一節。

## 錯誤修正 {#bug-fixes}

* 在某些情況下，內部系統同步失敗，導致資料視圖不一致。
* 在某些情況下，手動管線觸發器不會自動選取，而會導致表單驗證問題。
* 特定客戶建置指令碼可能會根據外掛程式不相容，在建置步驟中造成失敗。

## 已知問題 {#known-issues}

* 雖然客戶可以選擇提交觸發器，但管線可能不會基於新提交而實際啟動。
* 通知 [!UICONTROL Experience Cloud] 側欄可能無法一致地載入通知。 不過，通知會顯示在中， [!UICONTROL Experience Cloud] 且如果設定，仍會透過電子郵件傳送。

