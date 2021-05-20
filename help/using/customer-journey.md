---
title: 客戶歷程
seo-title: AdobeAEM Cloud Manager客戶歷程
description: 請詳閱本頁，了解您以客戶身分開始使用Cloud Manager的歷程。
seo-description: 請參閱本頁，了解您以客戶身分開始使用AdobeAEM Cloud Manager的歷程。
uuid: d4468eb6-5bde-48dd-b96e-0cc61e046f96
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: introduction
discoiquuid: bc9a0d63-ae6b-4fe9-81e5-bf9844f04e54
feature: 快速入門
level: Beginner
exl-id: deb3429c-dfcf-4e52-9aba-d9368aa240e6
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 2%

---

# 客戶歷程 {#customer-journey}

身為客戶，您可能是初次使用Adobe Experience Manager(AEM)、目前使用AEM 6.4的使用者，或者可能需要升級至AEM 6.4版本，才能使用[!UICONTROL Cloud Manager]。 下列案例說明您身為新客戶或現有客戶開始[!UICONTROL Cloud Manager]的歷程。

>[!NOTE]
>
>[!UICONTROL Cloud Manager] 僅適用於使用AEM 6.4或更新版本的Adobe Managed Services客戶。

## 上線至[!UICONTROL Cloud Manager]{#on-boarding-to-cloud-manager}

1. **Adobe Managed Services上的新AEM客戶**

   身為新客戶，您將上線至[!UICONTROL Cloud Manager]，作為Adobe Managed Services上線程的一部分。

   歡迎電子郵件會包含存取[!UICONTROL Cloud Manager]的URL，以及登入[!UICONTROL Experience Cloud]，並使用Adobe Admin Console來管理需要存取[!UICONTROL Cloud Manager]的使用者及其各自權限的指示。

1. **Adobe Managed Services上的現有AEM客戶**

   身為現有客戶，您必須先將現有的生產及非生產環境升級至AEM 6.4版。 同時，您將執行升級，並將上線並隨附存取[!UICONTROL Cloud Manager]的URL。 此外，您還需要針對需要存取[!UICONTROL Cloud Manager]的使用者，開始使用Adobe Admin Console來管理您的使用者及其個別權限。

   您現有的AEM專案也必須符合建議的最佳實務，因為您將開始使用[!UICONTROL Cloud Manager]將新程式碼變更部署至AEM環境。

   若要取得有關升級至AEM 6.4之優點的其他資訊，請參閱[升級至AEM 6.4](https://helpx.adobe.com/experience-manager/6-4/sites/deploying/using/upgrade.html)。

## 存取[!UICONTROL Cloud Manager] {#accessing-cloud-manager}

您只需登入[!UICONTROL Experience Cloud]登陸頁面、使用您的AdobeIdentity Management憑證，並從解決方案切換器介面選取AEM，即可存取[!UICONTROL Cloud Manager]和AEM環境。

首次登入[!UICONTROL Cloud Manager]後，您就能直接從[!UICONTROL Cloud Manager] UI存取AEM環境。 此時，您已準備好探索[!UICONTROL Cloud Manager]的所有可能性，只要您的第一個程式碼分支準備好部署至您的預備和生產環境即可。

若要探索並開始使用[!UICONTROL Cloud Manager]，請參閱[首次登入](first-time-login.md)。 如需AEM的其他資訊，請參閱[AEM 6.4](https://helpx.adobe.com/experience-manager/6-4/sites/deploying/using/deploy.html)快速入門。 此外，如需詳細資訊，請參閱[AEM資源](https://www.adobe.com/marketing-cloud/experience-manager/resources.html?promoid=759X6WV8&amp;mv=other)。

## [!UICONTROL Cloud Manager] {#getting-started-with-cloud-manager}快速入門

登入[!UICONTROL Cloud Manager]後，首先要做的就是設定程式碼存放庫環境，然後設定您的團隊和角色。 具體來說，角色成員資格的指派方式是使用Admin ConsoleUI將使用者新增至[!UICONTROL Cloud Manager]設定檔。

接下來，您必須在&#x200B;**Git存放庫**&#x200B;中設定原始碼分支，根據負載和效能KPI定義目標，並在所有品質檢查均成功通過後，測試藍本以成功將程式碼部署至預備和生產環境。

## 結束至結束歷程{#end-to-end-journey}

下圖說明使用[!UICONTROL Cloud Manager] CI/CD管道將程式碼變更部署至您的預備和生產環境時，客戶的高層歷程。

![](assets/screen_shot_2018-05-15at124004pm.png)
