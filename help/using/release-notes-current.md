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
* 現在可以下載監控圖形。 如需詳細 [資訊，請參閱](monitor-your-environments.md) 「監控您的環境」。
* 如果程式沒有生產AEM環境，從著陸頁面按一下程式卡會導覽至「雲端管理員概述」頁面，而不會產生錯誤對話方塊。
* 「概 **述」(Overview)頁** 面上的「管線設定」(Pipeline Settings **Card)已重新命名為「生產管** 線設定」(Production Pipeline Settings ****)。
* 「重要故障行為」選項按鈕已從僅代碼質量的管線中刪除。
* 「活 **動** 」頁面現在會顯示每個執行的管線名稱。
* 執行頁面現在會顯示管線的名稱。
* 「程式碼品質摘要」對話方塊現在會顯示每個評等的說明。

## 錯誤修正 {#bug-fixes}

* 有些使用者在等待核準時無法檢視執行詳細資訊。
* 在「 **概述** 」頁面上，右邊距不一致。
* 在大型專案中，建置容器可能會耗用記憶體。
* 在特定情況下，UnpardedPaths OakPAL規則未識別/libs下的已安裝內容。
* 拒絕質量門時，對話框標題仍顯示「部分 *通過」*。

## 已知問題 {#known-issues}

* Safari中無法下載監控圖表。
