---
title: 2019.9.0 版發行說明
seo-title: Cloud Manager AEM 2019.9.0發行說明
description: 請依照本頁取得Cloud Manager 2019.9.0版的相關資訊。
seo-description: 請依照本頁取得AEMCloud Manager 2019.9.0版的資訊。
feature: Release Information
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 5%

---

# 2019.9.0 版發行說明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2019.9.0版本會更新安全性測試標準、新增可下載的監控圖表，並修正客戶回報的可用性問題。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2019.9.0版的發行日期為2019年9月12日。

## 新功能 {#whats-new}

* Sling Referrer Filter Health check的分類已從Critical變更為Importent。
* HTML Library Manager Config運行狀況檢查的分類已從「Critical（關鍵）」更改為「Mignent（重要）」。
* 現在可以下載監控圖形。 有關詳細資訊，請參閱[監視環境](monitor-your-environments.md)。
* 如果程式沒有生產環AEM境，從著陸頁面按一下程式卡會導覽至「雲端管理員」概觀頁面，而不會產生錯誤對話方塊。
* **概述**&#x200B;頁面上的&#x200B;**管線設定**&#x200B;卡已改名為&#x200B;**生產管線設定**。
* 「重要故障行為」選項按鈕已從僅代碼質量的管線中刪除。
* **Activity**&#x200B;頁面現在會顯示每個執行的管線名稱。
* 執行頁面現在會顯示管線的名稱。
* 「程式碼品質摘要」對話方塊現在會顯示每個評等的說明。

## 錯誤修正 {#bug-fixes}

* 有些使用者在等待核準時無法檢視執行詳細資訊。
* 在&#x200B;**概述**&#x200B;頁面上，右邊距不一致。
* 在大型專案中，建置容器可能會耗用記憶體。
* 在特定情況下，UnpardedPaths OakPAL規則未識別/libs下的已安裝內容。
* 拒絕質量門時，對話框標題仍顯示&#x200B;*部分傳遞*。

## 已知問題 {#known-issues}

* Safari中無法下載監控圖表。
