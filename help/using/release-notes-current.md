---
title: 2019.9.0版發行說明
seo-title: 2019.9.0的AEM Cloud Manager發行說明
description: 請依照此頁面取得Cloud Manager發行2019.9.0的資訊。
seo-description: 請依照此頁面取得AEM Cloud Manager發行2019.9.0的資訊。
translation-type: tm+mt
source-git-commit: 548d18f251cf8c4c827d2208fec04cde235ce731

---

# 2019.9.0版發行說明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2019.9.0版本新增了Sling Referrer Filter health Check and monitoring Graphics的更新。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2019.9.0版的發行日期為2019年月11日。

## 新功能 {#whats-new}

* Sling Referrer Filter Health Check的分類已從重要變更為重要。
* HTML Library Manager組態健康檢查的分類已從重要變更為重要。
* 現在可以下載監控圖表。如需詳細資訊，請參閱 [監控您的環境](monitor-your-environments.md) 。
* 如果某個程式沒有生產AEM環境，從登陸頁面按一下程式卡片會導覽至Cloud Manager總覽頁面，而不會產生錯誤對話方塊。
* 「概述」頁面上的「管道設定資訊卡」已退役至 **「生產管道設定**」。
* 重要失敗行為選項按鈕已從僅限程式碼品質的管線移除。
* 活動頁面現在會顯示每個執行的管道名稱。
* 執行頁面現在會顯示管線名稱。
* 「程式碼品質摘要」對話方塊現在會顯示每個評分的說明。

## 錯誤修正 {#bug-fixes}

* 有些使用者在等待核准時無法檢視執行詳細資訊。
* 在「概述」頁面上，右側的邊界不一致。
* 大型專案中的建置容器可能記憶體不足。
* 在某些情況下，BandnedPath Oakcal規則無法識別已安裝內容在/libs下的位置。
* 當品質關卡遭到拒絕時，對話方塊標題仍會顯示「部分通過」。

## 已知問題 {#known-issues}

Safari無法下載監控圖表。
