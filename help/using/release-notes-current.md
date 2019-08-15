---
title: 2019.8.0版發行說明
seo-title: 2019.8.0AEM Cloud Manager發行說明
description: 請依照此頁面取得Cloud Manager發行2019.8.0的資訊。
seo-description: 請依照此頁面取得AEM Cloud Manager發行2019.8.0的資訊。
translation-type: tm+mt
source-git-commit: 365cd6dfe65059c0c529f774bbcda946d47b0db5

---

# 2019.8.0版發行說明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2019.8.0版本新增了選擇性建立的內容套件支援、改善建置效能，並修正了各種次要錯誤。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2019.8.0版的發行日期為2019年月19日。

## 新功能 {#whats-new}

* 由Adobe I/CLI提供的Cloud Manager [API新命令列介面](https://github.com/adobe/aio-cli-plugin-cloudmanager)。
* 建置的特定內容套件可能會宣告為可跳過，且不會部署。如需詳細資訊，請參閱建立AEM應用程式專案中 ******[的「Skipping Content](create-an-application-project.md) Packages」一節。
* 建置容器中的預先載入相依性集已重新運作，以避免某些不必要的網路要求。
* 部分錯誤設定程式的概述頁面上的訊息已改善。

## 錯誤修正 {#bug-fixes}

* 存取SLA報告時，預設年份為2018，而非2019。
* 對於長的環境名稱，報表畫面上的環境選擇器無法正確增加大小。
* ***當使用Sling Rewriter元件時，ConfigAndInstallShordlycontains*** 程式碼品質規則會產生錯誤的置信度。
* ***ConfigAndInstallShordonlyContainosyNode*** 程式碼品質規則針對某些不常見的路徑結構產生誤判。
* 僅限資產的客戶可能無法一致導覽至其AEM環境。
* [!UICONTROL Create a Branch and Project] 對話方塊以不同的瀏覽器呈現。
