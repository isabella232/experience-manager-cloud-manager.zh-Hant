---
title: 2019.8.0 版發行說明
seo-title: AEM Cloud Manager 2019.8.0版本注意事項
description: 請依照本頁取得Cloud Manager 2019.8.0版的相關資訊。
seo-description: 請依照本頁取得AEM Cloud Manager 2019.8.0版的相關資訊。
translation-type: tm+mt
source-git-commit: 2ada697ca21acd0c73dbce2bce3e9481ac50272c
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 5%

---

# 2019.8.0 版發行說明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2019.8.0版新增了對選擇性內建內容封裝的支援、改善內建效能，並修正了各種小錯誤。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2019.8.0版的發行日期為2019年8月19日。

## 新功能 {#whats-new}

* 由[Adobe I/O CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager)提供的Cloud Manager API新命令列介面。
* 由組建產生的特定內容封裝可宣告為已跳過且不會部署。 有關詳細資訊，請參閱[跳過內容包](/help/using/setting-up-project.md#skipping-content-packages)。
* 已重新處理建置容器中預先載入的相依性集，以避免某些不必要的網路要求。
* 某些配置錯誤的程式的概述頁面上的消息已經改進。

## 錯誤修正 {#bug-fixes}

* 存取SLA報告時，預設年份為2018，而非2019。
* 對於較長的環境名稱，「報告」畫面上的環境選擇器未正確增加大小。
* ***ConfigAndInstallShoudOnlyContainOsgiNodes***&#x200B;程式碼品質規則在使用Sling Rewriter元件時產生誤報。
* ***ConfigAndInstallShoudOnlyContainOsgiNodes***&#x200B;代碼品質規則會針對某些不常見的路徑結構產生誤報。
* 僅限資產的客戶可能無法一致地導覽至其AEM環境。
* 「建立分支」和「專案」對話方塊在不同瀏覽器上的呈現方式不同。
