---
title: 2019.8.0 版發行說明
seo-title: AEM Cloud Manager 2019.8.0版發行說明
description: 請詳閱本頁以取得Cloud Manager 2019.8.0版的資訊。
seo-description: 請詳閱本頁，以取得AEM Cloud Manager 2019.8.0版的資訊。
feature: 發行資訊
exl-id: 9b3da506-76f1-439f-8de0-a5e2ee88b979
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 6%

---

# 2019.8.0 版發行說明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2019.8.0版新增了對選擇性建置內容套件的支援、改善建置效能，並修正了各種小錯誤。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2019.8.0版的發行日期為2019年8月19日。

## 新功能 {#whats-new}

* 使用[Adobe I/OCLI](https://github.com/adobe/aio-cli-plugin-cloudmanager)提供的新命令列介面至Cloud Manager API。
* 組建產生的特定內容套件可宣告為已略過，且不會部署。 如需詳細資訊，請參閱[略過內容套件](/help/using/setting-up-project.md#skipping-content-packages) 。
* 組建容器中預先載入的相依性集已重作，以避免某些不必要的網路要求。
* 已改善「概述」頁面上針對某些未正確設定之程式所顯示的訊息。

## 錯誤修正 {#bug-fixes}

* 存取SLA報表時，預設年份為2018年，而非2019年。
* 若環境名稱較長，「報表」畫面上的環境選取器未正確增加大小。
* ***ConfigAndInstallShouldOnlyContainOsgiNodes***&#x200B;程式碼品質規則在使用Sling重寫器元件時產生誤判。
* ***ConfigAndInstallShouldOnlyContainOsgiNodes***&#x200B;代碼質量規則針對某些不常見的路徑結構產生誤判。
* 僅限資產的客戶可能無法一致地導覽至其AEM環境。
* 「建立分支」和「專案」對話方塊在不同瀏覽器間的呈現方式不同。
