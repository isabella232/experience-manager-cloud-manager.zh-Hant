---
title: 2018.5.0 版發行說明
seo-title: AEM Cloud Manager 2018.5.0版發行說明
description: 請詳閱本頁，以取得Cloud Manager 2018.5.0版的相關資訊。
seo-description: 請詳閱本頁，以取得AEM Cloud Manager 2018.5.0版的資訊。
uuid: 37f8b155-6984-454d-83a8-3f5fb081be97
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: release-notes
discoiquuid: 6d1e7098-b56e-4172-8373-486f186f3d53
feature: 發行資訊
exl-id: 0034bcaf-00d3-410d-b2f6-a2a232888a2b
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 8%

---

# 2018.5.0 版發行說明 {#release-notes-for}

以下章節概述[!UICONTROL Cloud Manager] 2018.5.0版的一般發行說明。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2018.5.0版的發行日期為2018年7月12日。

## 新功能 {#what-s-new}

* **CI/CD管道通知**  — 使用者現在會看到管 [!UICONTROL Experience Cloud] 道事件的通知。請參閱[通知](notifications.md)以了解更多資訊。

* **排程生產部署**  — 使用者現在可以為生產部署排程日期或時間。請參閱[部署程式碼](deploying-code.md)以深入了解。

* **** 狀態頁面已標題為 **活動**。

* 首頁上顯示的更多特定資訊，說明管道執行期間發生的問題。
* 效能測試基礎架構的改善。

## 錯誤修正 {#bug-fixes}

* 在某些情況下，會使用不正確的SonarQube設定檔，導致程式碼品質量度不正確。
* CQBP-75的聲納查詢忽略了某些OSGi注釋。
* 取消CI/CD管道時，狀態無法一致顯示。

## 已知問題 {#known-issues}

* 從程式清單螢幕指向&#x200B;**AEM**&#x200B;和&#x200B;**監視**&#x200B;的連結將替換當前瀏覽器頁簽並開啟到新頁簽。
