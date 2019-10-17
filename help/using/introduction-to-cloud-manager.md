---
title: Cloud Manager 簡介
seo-title: Cloud Manager 簡介
description: '本頁提供瞭解 Cloud Manager 的起始點。 '
seo-description: '本頁提供瞭解 Adobe AEM Cloud Manager 的起始點，並著重其優點和重要功能。 '
uuid: 62d68e79-c2ba-4d8b-ba7d-33709014d5b6
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: 簡介
discoiquuid: ebcc91a5-be9e-4684-8146-d88f4013d4d1
translation-type: ht
source-git-commit: d7c9ab3795fb3df02ab7dffd1328760ccd914a18

---


# [!UICONTROL Cloud Manager] 簡介{#introduction-to-cloud-manager}

## 簡介 {#introduction}

[!UICONTROL Cloud Manager]，是 Adobe Managed Cloud Services 的一部分，可讓組織在雲端自行管理 Experience Manager。其內容包含持續整合與持續傳送 (CI/CD) 架構，可讓 IT 團隊與實作合作夥伴加快提供自訂或更新的傳送速度，而不會影響效能或安全性。

使用 [!UICONTROL Cloud Manager] 自助服務客戶入口網站，**組織**&#x200B;便可以執行/善用以下內容: 

* **持續整合/持續傳送**&#x200B;程式碼，將上市時間從數月/數週縮短至數天/數小時。
* **程式碼檢查、效能測試和安全性驗證**，是根據最佳實務而設，然後再推送至生產環境，將生產中斷的情況降至最低。
* 即使在工作時間以外，也能&#x200B;**自動、排程或手動部署**，以發揮最大的彈性和控制能力。
* **自動縮放**&#x200B;功能，會聰明地偵測到增加容量的需求，並自動將其他 Dispatcher/Publish 區段連至網路。

下圖說明在 [!UICONTROL Cloud Manager] 中使用的 CI/CD 流程: 

![](assets/screen_shot_2018-05-12at73843pm.png)

## [!UICONTROL Cloud Manager] 中的重要功能 {#key-features-in-cloud-manager}

組織可透過 [!UICONTROL Cloud Manager] 運用下列功能: 

### 自助服務介面 {#self-service-interface}

適用於 [!UICONTROL Cloud Manager] 的使用者介面 (UI) 可讓客戶輕鬆存取和管理雲端環境，以及 Experience Manager 應用程式的 CI/CD 管道。

客戶定義應用程式專用的關鍵績效指標 (KPI) - 每分鐘尖峰頁面檢視次數，以及頁面載入的預期回應時間，而這些最終可構成衡量成功部署的基礎。您可以輕鬆定義不同團隊成員的角色和權限。全新的自助服務介面可讓您重新取得掌控，而且也提供最佳實務連結以及 Adobe 內部專家的存取權限，這些專家可提供您所需的指引。

若要探索並開始使用 [!UICONTROL Cloud Manager] 的 UI，請參閱[首次登入](https://helpx.adobe.com/tw/experience-manager/tw/cloud-manager/using/first-time-login.html)。

### CI/CD 管道 {#ci-cd-pipeline}

[!UICONTROL Cloud Manager] 的一項重要功能是可運用最佳化的 CI/CD 管道，以加速自訂程式碼或更新的傳送，例如在網站上新增元件。

透過 [!UICONTROL Cloud Manager] UI，客戶可以設定並啟動其 CI/CD 管道。在此管道期間，會執行徹底的程式碼掃描，以確保只有高品質的應用程式才能傳遞至生產環境。

若要進一步瞭解如何從 [!UICONTROL Cloud Manager] 的 UI 設定管道，請參閱[設定 CI/CD 管道](https://helpx.adobe.com/tw/experience-manager/cloud-manager/using/configuring-pipeline.html)。

### 有彈性的部署模式 {#flexible-deployment-modes}

[!UICONTROL Cloud Manager] 為客戶提供有彈性且可設定的部署模式，讓他們能夠根據不斷變化的業務需求提供體驗。

使用自動觸發模式時，程式碼會根據特定事件 (例如程式碼確認) 自動部署至環境。您也可以在指定的時間範圍內，甚至在工作時間以外，排程程式碼部署。

與部署觸發無關，每次觸發部署時都一律會執行品質檢查，作為 CI/CD 管道執行的一部分。品質檢查包括程式碼檢查、安全性測試和效能測試，為隨開即用的功能，客戶或其合作夥伴無需執行任何設定。

若要進一步瞭解部署程式碼和品質檢查，請參閱 [部署程式碼](deploying-code.md)

### 自動縮放 {#autoscaling}

[!UICONTROL Cloud Manager] 會在生產環境遭受到異常高的負載時，偵測到增加容量的需求，並透過自動縮放功能，自動將額外的容量連至網路。

在自動縮放的事件中，[!UICONTROL Cloud Manager] 會自動觸發自動縮放佈建程序，傳送自動縮放事件的通知，並在數分鐘內讓額外的容量上線。額外的容量會佈建在相同地區的生產環境中，並且採用與執行 Dispatcher/Publish 節點相同的系統規格。

自動縮放功能只會套用在 Dispatcher/Publish 層，而且一律會採用水平縮放的方法來執行，至少一個額外的 Dispatcher/Publish 組合區段，最多十個區段。佈建的額外容量會在十個工作天的期間內以手動縮放，實際時間長短由 CSE (客戶成功工程師) 決定。
