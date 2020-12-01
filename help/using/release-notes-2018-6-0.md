---
title: 2018.6.0 版發行說明
seo-title: AEM Cloud Manager 2018.6.0版本注意事項
description: 請瀏覽本頁，以取得Cloud Manager 2018.6.0版的資訊。
seo-description: 請依照本頁取得AEM Cloud Manager 2018.6.0版的相關資訊。
uuid: 211b6e1b-10fb-46b0-b591-44d5e44abd77
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: release-notes
discoiquuid: 8584f467-3e61-41ea-98e4-f79e68c86469
translation-type: tm+mt
source-git-commit: 15f75ca67c3d52ae511357c5b564daaa3d9def6b
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 3%

---


# 2018.6.0 版發行說明 {#release-notes-for}

下節概述[!UICONTROL Cloud Manager] 2018.6.0版的一般發行說明，並新增部署期間對發送器失效的支援、其他通知和可用性改進。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2018.6.0版的發行日期為2018年8月9日。

## 新功能 {#what-s-new}

* **CI/CD管線** -在CI/CD管線執行期間，舞台和生產上的可配置Dispatcher失效和快取刷新。請參閱[配置CI/CD Pipeline](configuring-pipeline.md)以瞭解更多資訊。

* **CI/CD管線** -在管線設定期間，現在可以定義管線在其中一個質量門中遇到重要故障時的行為方式。請參閱[配置CI/CD Pipeline](configuring-pipeline.md)以瞭解更多資訊。

* **CI/CD管線** -在管線設定期間，現在可以選擇是由CSE還是任何可用CSE執行CSE監督。請參閱[配置CI/CD Pipeline](configuring-pipeline.md)以瞭解更多資訊。

* **CI/CD管道** -當CI/CD管道進入業務批准步驟時，將向獲得批准部署授權的用戶發送通知。請參閱[通知](notifications.md)瞭解更多資訊。

* **CI/CD管道** -當CI/CD管道到達調度集時，將向有權設定調度的用戶發送通知。請參閱[通知](notifications.md)瞭解更多資訊。

* **程式碼品質分析** -用以識別未正確設定對外HTTP/HTTPS要求的新規則。請參閱[自訂程式碼品質規則](custom-code-quality-rules.md)以瞭解詳細資訊。

## 錯誤修正 {#bug-fixes}

* 在某些情況下，效能測試並未完全分佈於多個分發器和發佈執行個體。
* 頁首導覽在狹窄的瀏覽器視窗中消失。
* 在管線運行時，某些管線設定未禁用。
* 「AEM」和「從程式清單監視」畫面的連結會取代目前的瀏覽器標籤，並開啟新的標籤。
* 在某些情況下，長時間的核准期可能會導致部署失敗。
