---
title: 已佈建的環境
seo-title: 在AEM Cloud Manager中布建的環境
description: 請依照本頁來檢視Cloud Manager中提供的環境
seo-description: 請依照本頁來檢視AEM Cloud Manager中可用的布建環境。
uuid: d04ee39c-7112-4adc-ad4e-56f91cc4ecfa
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: requirements
discoiquuid: 7d32ba78-4ded-4656-aac2-c3e7cc0518de
translation-type: tm+mt
source-git-commit: ace032fbb26235d87d61552a11996ec2bb42abce
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 1%

---


# 已佈建的環境 {#environments-provisioned}

## 預配{#provisioning}

在客戶上線程式中，客戶購買的所有AEM雲端環境都會由Adobe自動布建，並連結回[!UICONTROL Cloud Manager]中的程式。 這些AEM Cloud **Environments**&#x200B;包含在每個Adobe Managed Services訂閱中，通常包含至少一個生產環境、一個階段環境，以及可選的一個或多個開發或測試環境。

## 歡迎寄電子郵件{#welcome-email}

在完成環境提供程式後，指定的客戶管理員會收到一封&#x200B;**歡迎電子郵件**，並確認他們已獲得Adobe [!UICONTROL Experience Cloud]的存取權。 電子郵件包含如何開始使用[!UICONTROL Experience Cloud]服務、[!UICONTROL AEM Managed Services]雲端環境以及[!UICONTROL Cloud Manager]自助服務入口網站的詳細資訊。 此外，電子郵件還包含重要資訊，例如客戶成功工程師聯絡資訊、支援資源、論壇或常見問答集的去向等。 在電子郵件中提供的資源清單中，您也會取得如何存取[!UICONTROL Cloud Manager]或AEM雲端環境的詳細資訊。

## 後續步驟{#next-steps}

收到歡迎電子郵件後，您就可以使用您的Adobe IMS認證，以管理員身分登入[!UICONTROL Cloud Manager]。 登入後，您將可以確認您的AEM雲端生產與非生產環境是否可用，並順利執行。

[!UICONTROL Cloud Manager]將會使用這些AEM雲端環境，在部署程式碼時，從[!UICONTROL Cloud Manager]的Git儲存庫開始，透過階移&#x200B;**Environment**&#x200B;執行CI/CD管道，直到您的AEM生產環境為止。 當您準備好開始為網頁屬性建立數位體驗時，您也可以直接從[!UICONTROL Cloud Manager]存取您的AEM雲端環境。
