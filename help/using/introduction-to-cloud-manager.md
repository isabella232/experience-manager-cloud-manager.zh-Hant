---
title: Cloud Manager 簡介
seo-title: Introduction to Cloud Manager
description: '本頁提供瞭解 Cloud Manager 的起始點。 '
seo-description: This page serves as a starting point for learning about Adobe AEM Cloud Manager and highlights the benefits and key features.
uuid: 62d68e79-c2ba-4d8b-ba7d-33709014d5b6
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: introduction
discoiquuid: ebcc91a5-be9e-4684-8146-d88f4013d4d1
feature: Getting Started
level: Beginner
exl-id: 58344d8a-b869-4177-a9cf-6a8b7dfe9588
source-git-commit: 08d831c560510d58062ed81fab809c12169810cb
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 66%

---

# [!UICONTROL Cloud Manager] 簡介{#introduction-to-cloud-manager}

>[!CONTEXTUALHELP]
>id="aemcloud_cloudmanager_introduction"
>title="Cloud Manager 簡介"
>abstract="可讓組織在雲端中自行管理Experience Manager。 其內容包含持續整合與持續傳送 (CI/CD) 架構，可讓 IT 團隊與實作合作夥伴加快提供自訂或更新的傳送速度，而不會影響效能或安全性。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=en#cloud-manager" text="建立方案"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=en#cloud-manager" text="建立環境"

## 簡介 {#introduction}

[!UICONTROL Cloud Manager] 針對Adobe Experience Manager，開發人員能透過以Adobe Experience Manager最佳實務為基礎的簡化工作流程，建立具影響力的客戶體驗。 針對Adobe Experience Manager最佳化的CI/CD管道，可讓您只要檢查程式碼並一路移至生產就緒，即可輕鬆合併開發工作流程。 在建置階段，您會使用經過嘗試和學習的最佳實務來徹底測試自訂程式碼更新，以為客戶提供具影響力的數位體驗。 Cloud Manager使用開放API方法，可讓您與系統整合，而不會中斷現有的程式和工具。

本檔案網站特別說明Cloud Manager for Adobe Managed Services(AMS)客戶的功能。 AEMas a Cloud Service客戶的相同檔案位於 [為AEMas a Cloud Service實作應用程式](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/home.html?lang=en).

透過Cloud Manager，您的開發團隊可善用下列功能：

* 持續整合/持續傳送程式碼，將上市時間從數月/數週縮短至數天/數小時。

* 程式碼檢查、效能測試和安全性驗證是根據最佳實務而設，然後再推送至生產環境，將生產中斷的情況降至最低。

* API連線，以補充現有的DevOps程式。

* 自動縮放功能，會聰明地偵測到增加容量的需求，並自動將其他 Dispatcher/Publish 區段連至網路。

下圖說明在 [!UICONTROL Cloud Manager] 中使用的 CI/CD 流程: 

![](assets/screen_shot_2018-05-12at73843pm.png)

## [!UICONTROL Cloud Manager] 中的重要功能  {#key-features-in-cloud-manager}

組織可透過 [!UICONTROL Cloud Manager] 運用下列功能: 

### 自助服務介面 {#self-service-interface}

適用於 [!UICONTROL Cloud Manager] 的使用者介面 (UI) 可讓客戶輕鬆存取和管理雲端環境，以及 Experience Manager 應用程式的 CI/CD 管道。

客戶定義應用程式專用的關鍵績效指標 (KPI) - 每分鐘尖峰頁面檢視次數，以及頁面載入的預期回應時間，而這些最終可構成衡量成功部署的基礎。您可以輕鬆定義不同團隊成員的角色和權限。全新的自助服務介面可讓您重新取得掌控，而且也提供最佳實務連結以及 Adobe 內部專家的存取權限，這些專家可提供您所需的指引。

探索並開始使用 [!UICONTROL Cloud Manager]的UI，請參閱 [首次登入](https://helpx.adobe.com/experience-manager/cloud-manager/using/first-time-login.html).

### CI/CD 管道 {#ci-cd-pipeline}

[!UICONTROL Cloud Manager] 的一項重要功能是可運用最佳化的 CI/CD 管道，以加速自訂程式碼或更新的傳送，例如在網站上新增元件。

透過 [!UICONTROL Cloud Manager] UI，客戶可以設定並啟動其 CI/CD 管道。在此管道期間，會執行徹底的程式碼掃描，以確保只有高品質的應用程式才能傳遞至生產環境。

若要進一步了解如何透過 [!UICONTROL Cloud Manager]的UI，請參閱 [設定CI/CD管道](https://helpx.adobe.com/experience-manager/cloud-manager/using/configuring-pipeline.html).

### 有彈性的部署模式 {#flexible-deployment-modes}

[!UICONTROL Cloud Manager] 為客戶提供有彈性且可設定的部署模式，讓他們能夠根據不斷變化的業務需求提供體驗。

使用自動觸發模式時，程式碼會根據特定事件 (例如程式碼確認) 自動部署至環境。您也可以在指定的時間範圍內，甚至在工作時間以外，排程程式碼部署。

與部署觸發無關，每次觸發部署時都一律會執行品質檢查，作為 CI/CD 管道執行的一部分。品質檢查包括程式碼檢查、安全性測試和效能測試，為隨開即用的功能，客戶或其合作夥伴無需執行任何設定。

若要進一步瞭解部署程式碼和品質檢查，請參閱 [部署程式碼](deploying-code.md)

### 自動縮放 {#autoscaling}

[!UICONTROL Cloud Manager] 會在生產環境遭受到異常高的負載時，偵測到增加容量的需求，並透過自動縮放功能，自動將額外的容量連至網路。

在自動縮放的事件中，[!UICONTROL Cloud Manager] 會自動觸發自動縮放佈建程序，傳送自動縮放事件的通知，並在數分鐘內讓額外的容量上線。額外的容量會佈建在相同地區的生產環境中，並且採用與執行 Dispatcher/Publish 節點相同的系統規格。

自動縮放功能只會套用在 Dispatcher/Publish 層，而且一律會採用水平縮放的方法來執行，至少一個額外的 Dispatcher/Publish 組合區段，最多十個區段。佈建的額外容量會在十個工作天的期間內以手動縮放，實際時間長短由 CSE (客戶成功工程師) 決定。

>[!NOTE]
>想要探索自動縮放是否適合其應用程式的客戶，必須聯絡其CSE或Adobe代表。
