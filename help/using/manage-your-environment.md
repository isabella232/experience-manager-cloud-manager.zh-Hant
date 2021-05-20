---
title: 管理環境
seo-title: 管理環境
description: 了解Cloud Manager環境
seo-description: 請依照本頁面所述，檢視在Cloud Manager中設定及執行CI/CD管道時，所使用的生產及非生產環境清單。
uuid: 04e67572-11db-4d5d-acf3-fd7f644a95f0
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
discoiquuid: c5b39de2-3a9b-437f-98e8-e6e6249a5b3a
feature: 環境
exl-id: 700b0b4c-1e1a-4993-b366-426b14a98f8e
source-git-commit: df2f598f91201d362f54b17e4092ff6bd6a72cec
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 3%

---

# 管理環境 {#manage-your-environments}

>[!NOTE]
>若要了解如何在AEM as aCloud Service中管理Cloud Manager的環境，請參閱[此處](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=en#using-cloud-manager)。

Cloud Manager的&#x200B;**概述**&#x200B;頁面包含&#x200B;**Environments**&#x200B;圖磚，其中會列出所有受管理的AEM環境。

列出的每個環境都會顯示其關聯狀態。

![](assets/Manage-Environ-Overview.png)

## 影片教學課程{#video-tutorial}

### Cloud Manager環境概述{#environ-video}

以下影片提供由AEM Author、AEM Publish和Dispatcher例項組成之Cloud Manager環境的概觀。

>[!VIDEO](https://video.tv.adobe.com/v/26318/)

## 在Cloud Manager {#accessing-environments-in-cloud-manager}中存取環境

「**環境**」表徵圖顯示程式中布建的生產和階段環境以及狀態。

狀態是環境中各個節點的累計電源狀態。 如果所有節點都在運行，則為綠色；如果某個節點停止，則為紅色；如果某個節點出現，則為藍色；如果某個節點的電源狀態不可用，則為黃色（按照此優先順序）。

![](assets/Environments-card-new.png)

### 環境 {#environments}

按一下&#x200B;**管理**&#x200B;以顯示&#x200B;**環境**&#x200B;畫面。

**Environments**&#x200B;螢幕顯示程式中每個&#x200B;*Production*&#x200B;和&#x200B;*Stage*&#x200B;環境（如適用）的卡片。 每張卡片上方會顯示環境名稱。 該卡包括環境中的節點表，以及cpu的t恤大小、儲存、區域和狀態。

>[!NOTE]
>
>節點的&#x200B;**STATUS**&#x200B;表示VM的電源狀態，不反映伺服器上AEM的狀態。 狀態可以是&#x200B;**正在運行**（綠色圓）、**已停止**（紅色圓）、**正在運行**（藍色圓）或&#x200B;**不可用**（黃色圓）。

![](assets/Environments-tab.png)
