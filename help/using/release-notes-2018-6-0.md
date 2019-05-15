---
title: 2018.6.0版發行說明
seo-title: 2018.6.0AEM Cloud Manager發行說明
description: 將此頁面設為可取得Cloud Manager發行2018.6.0的資訊。
seo-description: 請依照此頁面取得AEM Cloud Manager發行2018.6.0的資訊。
uuid: 211b6e1b-10fb-46b0-b591-44d5 e44 abd77
contentOwner: jsyal
products: SG_ PERIENCENCENAGER/CLUDManager
topic-tags: 版本注意事項
discoiquuid: 8584f467-3e61-41ea-98e4-f79 e68 c86469
translation-type: tm+mt
source-git-commit: 1dfb065c09569f811e5a006d3d74825d3bd7cc8d

---


# 2018.6.0版發行說明 {#release-notes-for}

下節概述 [!UICONTROL Cloud Manager] 2018.6.0版的一般發行說明，並新增部署期間的排程器失效、額外通知和可用性改進的支援。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2018.6.0版的發行日期為2018年月日。

## 新功能 {#what-s-new}

* **CI/CD管道** -可設定的Dispatcher失效和快取在CI/CD管線執行期間同時在舞台和生產中刷新。請參閱 [設定您的CI/CD管線](configuring-pipeline.md) 以瞭解更多資訊。

* **CI/CD管道** -在管線設定期間，現在可以定義管線在一個品質關卡中遇到重大故障時的行為方式。請參閱 [設定您的CI/CD管線](configuring-pipeline.md) 以瞭解更多資訊。

* **CI/CD管道** -在管線設定期間，現在可以選取您是否要由CSE或任何可用的CSE執行CSE監督。請參閱 [設定您的CI/CD管線](configuring-pipeline.md) 以瞭解更多資訊。

* **CI/CD管道** -當CI/CD管道到達商業核准步驟時，會傳送通知給獲授權批准部署的使用者。請參閱 [通知](notifications.md) 以瞭解更多資訊。

* **CI/CD管道** -當CI/CD管道到達排程設定時，會傳送通知給獲得授權設定排程的使用者。請參閱 [通知](notifications.md) 以瞭解更多資訊。

* **程式碼品質分析** -識別錯誤配置傳出HTTP/HTTPS請求的新規則。請參閱 [自訂代碼品質規則](custom-code-quality-rules.md) 以瞭解更多資訊。

## 錯誤修正 {#bug-fixes}

* 在某些情況下，效能測試並未完整分配給多個分派程式和發佈例項。
* 頁首導覽在縮小的瀏覽器視窗中消失。
* 在執行管道時，有些管道設定不會停用。
* 「AEM從Program」清單畫面的連結取代了目前的瀏覽器標籤並開啓了新的標籤。
* 在某些情況下，長時間執行核准可能會導致部署失敗。
