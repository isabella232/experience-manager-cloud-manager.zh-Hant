---
title: 2019.9.0 版發行說明
seo-title: AEM Cloud Manager 2019.9.0版發行說明
description: 請詳閱本頁以取得Cloud Manager 2019.9.0版的資訊。
seo-description: 請詳閱本頁以取得AEM Cloud Manager 2019.9.0版的資訊。
feature: 發行資訊
exl-id: 0aaf969a-f4f9-441b-8b17-7ac2f9b9ad50
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 5%

---

# 2019.9.0 版發行說明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2019.9.0版更新安全性測試標準、新增可下載的監控圖表，並修正一些客戶回報的可用性問題。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2019.9.0版的發行日期為2019年9月12日。

## 新功能 {#whats-new}

* Sling反向連結篩選器健全狀態檢查的分類已從「重要」變更為「重要」。
* HTML Library Manager配置運行狀況檢查的分類已從「關鍵」更改為「重要」。
* 現在可以下載監控圖表。 如需詳細資訊，請參閱[監視環境](monitor-your-environments.md) 。
* 如果程式沒有生產AEM環境，請從登陸頁面按一下程式卡片會導覽至Cloud Manager概觀頁面，但不會產生錯誤對話方塊。
* **概述**&#x200B;頁面上的&#x200B;**管道設定**&#x200B;卡片已更名為&#x200B;**生產管道設定**。
* 「重要失敗行為」選項按鈕已從僅限程式碼品質的管道中移除。
* **Activity**&#x200B;頁面現在會顯示每個執行的管道名稱。
* 執行頁面現在會顯示管道名稱。
* 「代碼品質摘要」對話方塊現在會顯示每個評等的說明。

## 錯誤修正 {#bug-fixes}

* 當某些用戶等待批准時，無法查看執行詳細資訊。
* 在&#x200B;**概述**&#x200B;頁面上，右邊界不一致。
* 大型專案中的組建容器可能會耗盡記憶體。
* 在特定情況下，UnpandedPaths OakPAL規則不會識別/libs下的已安裝內容。
* 拒絕質量門時，對話框標題仍顯示&#x200B;*Partial Passed*。

## 已知問題 {#known-issues}

* Safari中無法下載監控圖形。
