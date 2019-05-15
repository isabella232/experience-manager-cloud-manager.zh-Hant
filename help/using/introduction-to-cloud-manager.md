---
title: Cloud Manager簡介
seo-title: Cloud Manager簡介
description: '此頁面是瞭解Cloud Manager的起點。 '
seo-description: '此頁面是瞭解Adobe AEM Cloud Manager的起點，並強調了優點和主要功能。 '
uuid: 62d68e79-c2 ba-4d8 b-ba7 d-33709014d5 b6
contentOwner: jsyal
products: SG_ PERIENCENCENAGER/CLUDManager
topic-tags: 簡介
discoiquuid: ebcc91a5-be9 e-4684-8146-d88 f4013 d4 d1
translation-type: tm+mt
source-git-commit: 1dfb065c09569f811e5a006d3d74825d3bd7cc8d

---


# 簡介 [!UICONTROL Cloud Manager]{#introduction-to-cloud-manager}

## 簡介 {#introduction}

[!UICONTROL Cloud Manager](屬於Adobe Managed Cloud Services的一部分)可讓組織自行管理雲端的Experience Manager。它包含持續整合和持續提供(CI/CD)架構，可讓IT團隊和實作合作夥伴加速交付自訂或更新，而不會影響效能或安全性。

使用 [!UICONTROL Cloud Manager] 自助服務客戶入口網站 **，組織** 可以執行/運用下列各項：

* **持續整合/持續提供** 程式碼，將上市時間從數月/數周縮短為數天/數小時。
* **程式碼檢查、效能測試和基於最佳實務的安全性驗證** ，再推送至生產環境，將生產中斷降至最低。
* **即使在營業時間以外，也能自動、排程或手動部署** ，提供最大的彈性和控制力。
* **自動啓動** 功能會聰明地偵測增加容量，並自動帶入線上額外的Dispatcher/發佈區段。

下圖說明 [!UICONTROL Cloud Manager]用於：

![](assets/screen_shot_2018-05-12at73843pm.png)

## 主要功能 [!UICONTROL Cloud Manager]{#key-features-in-cloud-manager}

組織可利用下列功能， [!UICONTROL Cloud Manager]其中包括：

### 自助服務介面 {#self-service-interface}

使用者介面(UI)可 [!UICONTROL Cloud Manager] 讓客戶輕鬆存取及管理Experience Manager應用程式的雲端環境和CI/CD管線。

客戶定義應用程式特定關鍵績效指標(KPI)-每分鐘峰值頁面檢視次數，以及頁面載入的預期回應時間，最終構成測量成功部署的基礎。可以輕鬆定義不同團隊成員的角色和權限。全新的自助服務介面可讓您掌握掌控權，同時也提供最佳實務的連結，以及Adobe內部專家的存取權限，讓他們可視需要提供必要的指導。

若要探索並開始使用 [!UICONTROL Cloud Manager]UI，請參閱 [首次登入](https://helpx.adobe.com/experience-manager/cloud-manager/using/first-time-login.html)。

### CI/CD管線 {#ci-cd-pipeline}

其主要功能之一 [!UICONTROL Cloud Manager] ，就是執行最佳化的CI/CD管線，以加速傳送自訂程式碼或更新，例如在網站上新增元件。

透過 [!UICONTROL Cloud Manager] UI，客戶可以設定並啓動他們的CI/CD管線。在此管道期間，會執行完整的程式碼掃描，以確保只有高品質的應用程式才能傳遞到生產環境。

如需深入瞭解從UI設定管道的詳細 [!UICONTROL Cloud Manager]資訊，請參閱 [設定您的CI/CD管線](https://helpx.adobe.com/experience-manager/cloud-manager/using/configuring-pipeline.html)。

### 彈性的部署模式 {#flexible-deployment-modes}

[!UICONTROL Cloud Manager] 為客戶提供彈性而可設定的部署模式，讓他們根據不斷變化的業務需求提供體驗。

使用自動觸發模式，程式碼會根據特定事件(例如程式碼提交)自動部署至環境。您也可以在指定時間範圍內排程程式碼部署，即使是在營業時間之外。

在每次觸發部署時，品質檢查一律會在CI/CD管線執行階段中執行。品質檢查包括從包裝盒中提供的程式碼檢查、安全性測試以及效能測試，不需要客戶或其合作夥伴的努力。

若要進一步瞭解部署程式碼和品質檢查，請參閱 [部署程式碼](deploying-code.md)

### 自動上色 {#autoscaling}

[!UICONTROL Cloud Manager] 偵測到製作環境可能會受到異常高負載的影響，並自動透過自動調整功能在線上提供額外容量。

自動調整事件時 [!UICONTROL Cloud Manager] ，自動觸發自動調整布建程序、傳送自動調整事件的通知，並在幾分鐘內開啓額外容量。在生產環境中，將會在生產環境中布建額外容量，並符合與執行Dispatcher/Publish節點相同的系統規格。

自動調整功能只會套用至Dispatcher/Publish層，而且一律會使用水平縮放方法執行，最少可使用Dispatcher/Publish配對的一個區段，最多可使用10個區段。任何額外的容量都將在CSE(客戶成功工程師)確定的10個工作天內手動調整。
