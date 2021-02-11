---
title: 2018.7.0 版發行說明
seo-title: 2018.7.0 版發行說明
description: 瞭解Cloud Manager 2018.7.0版
seo-description: 請依照本頁取得Cloud Manager 2018.7.0版的相關資訊。
uuid: d7b49e32-01dc-48ce-b744-e6a806fbdd8a
contentOwner: jsyal
topic-tags: release-notes
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
discoiquuid: b64bf9ab-27ed-4f33-adc8-d73d34094f1b
translation-type: tm+mt
source-git-commit: 2dda85baa5e7ed9bfd8933df3580ec6fc3c210fd
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 12%

---


# 2018.7.0 版發行說明 {#release-notes-for}

下節概述[!UICONTROL Cloud Manager] 2018.7.0版本，其中提供&#x200B;*自動縮放*&#x200B;功能。

**自動擴充功能是透過生產環境中 區段的橫向擴充功能來啟用，用於支援突然增加的負載、磁碟區、存取和其他已定義的監控量度。**`Dispatcher/Publish`

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2018.7.0版的發行日期為2018年9月10日。

## 新功能 {#what-s-new}

* **布建** -現 [!UICONTROL Cloud Manager] 在可以使用Dispatcher/Publish細分水準向外擴展，從而自動擴展客戶程式上的生產環境。UI中的新功能是「方案設定」中的「布建」區段，如果在客戶方案上啟用自動縮放，則會顯示此區段。 請參閱[設定您的計畫](setting-up-program.md)以瞭解更多資訊。

* **環境** -現在可以詳細查看生產和階段環境以及與每個環境相關聯的節點的大小、儲存、區域和狀態。請參閱[管理您的環境](manage-your-environment.md)以瞭解更多資訊。

* **程式碼品質分析** -用以識別錯誤API使用情形的新規則。請參閱[自訂程式碼品質規則](custom-code-quality-rules.md)以瞭解詳細資訊。

* **效能測試** -在查看效能測試結果時，可獲得CPU利用率、磁碟I/O等待時間、頁錯誤率、磁碟頻寬利用率、網路頻寬利用率、峰值頁面響應時間和第95個百分位數頁面響應時間的圖表。請參閱[瞭解測試結果](understand-your-test-results.md)頁面上的&#x200B;*效能測試*&#x200B;一節。

* **效能測試** -檢視效能測試結果時，可下載頁面錯誤和慢速請求的清單。請參閱[瞭解測試結果](understand-your-test-results.md)頁面上的&#x200B;*效能測試*&#x200B;一節。

## 錯誤修正 {#bug-fixes}

* 在某些情況下，內部系統同步失敗，導致資料視圖不一致。
* 在某些情況下，手動管線觸發器不會自動選取，而會導致表單驗證問題。
* 特定客戶建置指令碼可能會根據外掛程式不相容，在建置步驟中造成失敗。

## 已知問題 {#known-issues}

* 雖然客戶可以選擇提交觸發器，但管線可能不會基於新提交而實際啟動。
* [!UICONTROL Experience Cloud]通知邊欄可能無法一致地載入通知。 但是，通知會顯示在[!UICONTROL Experience Cloud]中，若已設定，仍會透過電子郵件傳送。

