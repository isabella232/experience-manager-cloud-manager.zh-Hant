---
title: 2018.6.0 版發行說明
seo-title: AEM Cloud Manager 2018.6.0版發行說明
description: 請詳閱本頁以取得Cloud Manager 2018.6.0版的資訊。
seo-description: 請詳閱本頁，以取得AEM Cloud Manager 2018.6.0版的資訊。
uuid: 211b6e1b-10fb-46b0-b591-44d5e44abd77
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: release-notes
discoiquuid: 8584f467-3e61-41ea-98e4-f79e68c86469
feature: 發行資訊
exl-id: 456f7892-c64c-4b3f-b845-15682d034aaa
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 4%

---

# 2018.6.0 版發行說明 {#release-notes-for}

以下章節概述[!UICONTROL Cloud Manager] 2018.6.0版的一般發行說明，並新增對部署期間Dispatcher失效、其他通知和可用性改善的支援。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2018.6.0版的發行日期為2018年8月9日。

## 新功能 {#what-s-new}

* **CI/CD管道**  — 在CI/CD管道執行期間，預備和生產上的可設定Dispatcher失效和快取排清。請參閱[設定CI/CD管道](configuring-pipeline.md)以深入了解。

* **CI/CD管道**  — 在管道設定期間，現在可定義管道在其中一個品質閘道中遇到重要故障時的行為。請參閱[設定CI/CD管道](configuring-pipeline.md)以深入了解。

* **CI/CD管道**  — 在管道設定期間，現在可以選擇您希望CSE或任何可用CSE執行CSE監督。請參閱[設定CI/CD管道](configuring-pipeline.md)以深入了解。

* **CI/CD管道**  — 當CI/CD管道達到業務核准步驟時，會傳送通知給獲授權核准部署的使用者。請參閱[通知](notifications.md)以了解更多資訊。

* **CI/CD管道**  — 當CI/CD管道達到排程集時，會傳送通知給獲授權設定排程的使用者。請參閱[通知](notifications.md)以了解更多資訊。

* **程式碼品質分析**  — 識別設定不正確之傳出HTTP/HTTPS要求的新規則。請參閱[自訂程式碼品質規則](custom-code-quality-rules.md)以深入了解。

## 錯誤修正 {#bug-fixes}

* 在某些情況下，效能測試並未完全分散在多個Dispatcher和發佈例項之間。
* 窄瀏覽器窗口上的標題導航消失。
* 管道執行期間未停用某些管道設定。
* 指向AEM和從程式清單螢幕的連結替換了當前瀏覽器頁簽並開啟了新頁簽。
* 在某些情況下，長時間的批准期可能導致部署失敗。
