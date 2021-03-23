---
title: 管理環境
seo-title: 管理環境
description: 瞭解Cloud Manager環境
seo-description: 請依照本頁查看用於在Cloud Manager中設定和運行CI/CD管道的生產和非生產環境的清單。
uuid: 04e67572-11db-4d5d-acf3-fd7f644a95f0
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
discoiquuid: c5b39de2-3a9b-437f-98e8-e6e6249a5b3a
feature: 環境
translation-type: tm+mt
source-git-commit: c5d32d49782c899d013fcc60b9c4d2b67e9350ae
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 4%

---


# 管理環境 {#manage-your-environments}

Cloud Manager的&#x200B;**概述**&#x200B;頁面包含列出所有受管理環境的&#x200B;**環境** AEM表徵圖。

每個列出的環境都顯示其關聯狀態。

![](assets/Manage-Environ-Overview.png)

## 教學影片{#video-tutorial}

### Cloud Manager環境概述{#environ-video}

以下影片提供由AEM Author、AEM Publish和Dispatcher例項組成的Cloud Manager環境概觀。

>[!VIDEO](https://video.tv.adobe.com/v/26318/)

## 訪問Cloud Manager中的環境{#accessing-environments-in-cloud-manager}

**Environments**&#x200B;方塊會顯示您的程式中布建的「生產」和「舞台」環境以及狀態。

狀態是環境中節點上累計的電源狀態。 如果所有節點都在運行，則為綠色；如果某個節點停止，則為紅色；如果某個節點出現，則為藍色；如果某個節點的電源狀態不可用，則為黃色（按此優先順序順序）。

![](assets/Environments-card-new.png)

### 環境 {#environments}

按一下&#x200B;**管理**&#x200B;以顯示&#x200B;**環境**&#x200B;螢幕。

**Environments**&#x200B;螢幕會針對您的程式中的&#x200B;*Production*&#x200B;和&#x200B;*Stage*&#x200B;環境顯示一張卡片（視適用情況而定）。 每張卡片上方會顯示環境名稱。 該卡包括環境中的節點表，以及CPU的t恤大小、儲存、區域和狀態。

>[!NOTE]
>
>節點的&#x200B;**STATUS**&#x200B;表示VM的電源狀態，不反映伺服器AEM的狀態。 狀態可以是&#x200B;**運行**（綠色圓）、**停止**（紅色圓）、**啟動**（藍色圓）或&#x200B;**不可用**（黃色圓）。

![](assets/Environments-tab.png)
