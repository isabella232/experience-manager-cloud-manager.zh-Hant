---
title: Cloud manager簡介
seo-title: Cloud manager簡介
description: '本頁是您瞭解Cloud manager的起點。 '
seo-description: '本頁面是您瞭解Adobe AEM Cloud manager的起點，並著重說明其優點和主要功能。 '
uuid: 62d68e79-c2ba-4d8b-ba7d-33709014d5b6
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: 簡介
discoiquuid: ebcc91a5-be9e-4684-8146-d88f4013d4d1
translation-type: tm+mt
source-git-commit: d7c9ab3795fb3df02ab7dffd1328760ccd914a18

---


# 簡介 [!UICONTROL Cloud Manager]{#introduction-to-cloud-manager}

## 簡介 {#introduction}

[!UICONTROL Cloud Manager]Adobe Managed Cloud services的一部分，讓組織能夠在雲端自行管理Experience Manager。 它包含持續整合與持續傳送(CI/CD)架構，讓IT團隊與實施合作夥伴加速自訂或更新的傳送，而不會影響效能或安全性。

使用自 [!UICONTROL Cloud Manager] 助服務客戶門戶， **組織可以執行** /利用以下內容：

* **持續整合／持續傳送程式碼** ，將上市時間從數月／數週縮短至數天／小時。
* **程式碼檢查、效能測試和安全性驗證** ，先根據最佳實務進行，再推送至生產環境，將生產中斷降至最低。
* **即使在工作時間以外** ，也能自動、排程或手動部署，以發揮最大的彈性和控制力。
* **自動縮放功能** ，可智慧地檢測對增加容量的需求，並自動將其他Dispatcher/Publish區段帶入線上。

下圖說明了中使用的CI/CD流程 [!UICONTROL Cloud Manager]:

![](assets/screen_shot_2018-05-12at73843pm.png)

## 中的主要功能 [!UICONTROL Cloud Manager]{#key-features-in-cloud-manager}

組織可運用下列功能，包括 [!UICONTROL Cloud Manager]:

### 自助服務介面 {#self-service-interface}

適用於客戶的使用者介面(UI) [!UICONTROL Cloud Manager] 可讓客戶輕鬆存取和管理雲端環境，以及Experience manager應用程式的CI/CD管道。

客戶定義應用程式專用的關鍵績效指標(KPI)-每分鐘尖峰頁面檢視次數，以及頁面載入的預期回應時間，這最終構成衡量成功部署的基礎。 您可以輕鬆定義不同團隊成員的角色和權限。 雖然全新的自助服務介面可讓您重新掌控，但它也提供最佳實務連結，並讓Adobe內部的專家可視需要提供所需的指引。

若要探索並開始使用 [!UICONTROL Cloud Manager]UI，請參 [閱首次登入](https://helpx.adobe.com/experience-manager/cloud-manager/using/first-time-login.html)。

### CI/CD管道 {#ci-cd-pipeline}

其中一項主要功能 [!UICONTROL Cloud Manager] 是可運用最佳化的CI/CD管道，以加速自訂程式碼或更新的傳送，例如在網站上新增元件。

透過 [!UICONTROL Cloud Manager] UI，客戶可以設定並啟動其CI/CD管道。 在此管道期間，會執行徹底的程式碼掃描，以確保只有高品質的應用程式才能傳遞至生產環境。

若要進一步瞭解如何從UI設 [!UICONTROL Cloud Manager]定管道，請參 [閱設定CI/CD管道](https://helpx.adobe.com/experience-manager/cloud-manager/using/configuring-pipeline.html)。

### 有彈性的部署模式 {#flexible-deployment-modes}

[!UICONTROL Cloud Manager] 為客戶提供有彈性且可設定的部署模式，讓他們能夠根據不斷變化的業務需求提供體驗。

使用自動觸發模式時，程式碼會根據特定事件（例如程式碼提交）自動部署至環境。 您也可以在指定的時間範圍內，甚至在外部工作時間內，排程程式碼部署。

在每次觸發部署時，質量檢查始終作為CI/CD流水線執行的一部分執行，而與部署觸發器無關。 品質檢查包括程式碼檢查、安全性測試和立即可用的效能測試，完全不需要客戶或其合作夥伴的投入。

若要進一步瞭解如何部署程式碼和品質檢查，請參閱「部 [署程式碼」](deploying-code.md)

### 自動縮放 {#autoscaling}

[!UICONTROL Cloud Manager] 當生產環境承受異常高的負載時，會偵測到需要額外容量，並透過自動縮放功能自動將額外容量帶入線上。

在自動縮放事件 [!UICONTROL Cloud Manager] 期間，自動觸發自動縮放設定過程，發送自動縮放事件的通知，並在幾分鐘內線上提供附加容量。 將在生產環境中，在相同的區域中配置額外容量，並與運行的Dispatcher/Publish節點匹配相同的系統規範。

自動縮放功能將僅應用於Dispatcher/Publish層，並且始終使用水準縮放方法執行，Dispatcher/Publish對中至少有一個附加段，最多10個段。 根據CSE（客戶成功工程師）的判斷，任何額外容量將在10個工作天內手動擴展。
