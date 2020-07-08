---
title: 2019.8.0 版發行說明
seo-title: AEM Cloud Manager 2019.8.0版本注意事項
description: 請依照本頁取得Cloud Manager 2019.8.0版的相關資訊。
seo-description: 請依照本頁取得AEM Cloud Manager 2019.8.0版的相關資訊。
translation-type: tm+mt
source-git-commit: c07e88564dc1419bd0305c9d25173a8e0e1f47cf
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 5%

---

# 2019.8.0 版發行說明 {#release-notes-for}

2019.8.0 [!UICONTROL Cloud Manager] 版本新增了對選擇性內建內容封裝的支援、改善內建效能並修正多種次要錯誤。

## 發行日期 {#release-date}

2019.8.0版 [!UICONTROL Cloud Manager] 的發行日期為2019年8月19日。

## 新功能 {#whats-new}

* 由 [Adobe I/O CLI提供的Cloud Manager API新命令列介面](https://github.com/adobe/aio-cli-plugin-cloudmanager)。
* 構建版本生成的特定內容包可聲明為可跳過，且不會部署。 如需詳細 ***資訊，請參閱「建立AEM應用程*** 式專案」中的「跳過內容套件 [](/help/using/create-an-application-project.md) 」一節。
* 已重新處理建置容器中預先載入的相依性集，以避免某些不必要的網路要求。
* 某些配置錯誤的程式的概述頁面上的消息已經改進。

## 錯誤修正 {#bug-fixes}

* 存取SLA報告時，預設年份為2018，而非2019。
* 對於較長的環境名稱，「報告」畫面上的環境選擇器未正確增加大小。
* 當使 ***用Sling Rewriter元件時，ConfigAndInstallShowOnlyContainOsgiNodes*** code quality rule會產生誤報。
* ConfigAndInstallShoudOnlyContainOsgiNodes ****** 代碼品質規則針對某些不常見的路徑結構產生誤報。
* 僅限資產的客戶可能無法一致地導覽至其AEM環境。
* 「建立分支」和「專案」對話方塊在不同瀏覽器上的呈現方式不同。
