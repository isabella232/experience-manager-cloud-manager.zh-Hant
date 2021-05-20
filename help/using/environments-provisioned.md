---
title: 已佈建的環境
seo-title: 在AEM Cloud Manager中布建的環境
description: 請依照本頁所述，檢視Cloud Manager中可用的布建環境
seo-description: 請依照本頁面所述，檢視AEM Cloud Manager中可用的布建環境。
uuid: d04ee39c-7112-4adc-ad4e-56f91cc4ecfa
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: requirements
discoiquuid: 7d32ba78-4ded-4656-aac2-c3e7cc0518de
feature: 環境，布建
exl-id: eade4255-89b5-4c65-a498-1c6d4e8c73ff
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 1%

---

# 已佈建的環境 {#environments-provisioned}

## 布建 {#provisioning}

在客戶上線程式期間，客戶購買的所有AEM雲端環境都會由Adobe自動布建，並連結回[!UICONTROL Cloud Manager]中的計畫。 這些AEM雲&#x200B;**環境**&#x200B;包含在每個Adobe Managed Services訂閱中，通常由至少一個生產環境、一個階段環境，以及可選的一個或多個開發或測試環境組成。

## 歡迎電子郵件{#welcome-email}

在完成環境預配過程後，指定的客戶管理員將收到&#x200B;**歡迎電子郵件**，並確認他們已被授予對Adobe[!UICONTROL Experience Cloud]的訪問權。 電子郵件包含如何開始使用[!UICONTROL Experience Cloud]服務、[!UICONTROL AEM Managed Services]雲端環境，以及[!UICONTROL Cloud Manager]自助入口網站的詳細資訊。 此外，電子郵件還包含重要資訊，例如客戶成功工程師聯繫資訊、支援資源、論壇或常見問題集的去向等。 在電子郵件中提供的資源清單中，您也會取得如何存取[!UICONTROL Cloud Manager]或AEM雲端環境的詳細資訊。

## 後續步驟{#next-steps}

收到歡迎電子郵件後，您就可以使用您的AdobeIMS憑證，以管理員身分登入[!UICONTROL Cloud Manager]。 登入後，您將可以確認您的AEM雲端生產及非生產環境可供使用，並成功執行。

部署程式碼時，[!UICONTROL Cloud Manager]會使用這些AEM雲端環境，從[!UICONTROL Cloud Manager]的Git存放庫開始，透過測試&#x200B;**環境**，直到您的AEM生產環境為止，執行CI/CD管道。 當您準備好為Web屬性建立數位體驗時，您也可以直接從[!UICONTROL Cloud Manager]存取AEM雲端環境。
