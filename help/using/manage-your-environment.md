---
title: 管理環境
seo-title: Manage your Environments
description: 瞭解Cloud Manager環境
seo-description: Follow this page to view the list of production and non-production environments that are used for setting up and running the CI/CD pipeline in Cloud Manager.
uuid: 04e67572-11db-4d5d-acf3-fd7f644a95f0
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
discoiquuid: c5b39de2-3a9b-437f-98e8-e6e6249a5b3a
feature: Environments
exl-id: 700b0b4c-1e1a-4993-b366-426b14a98f8e
source-git-commit: 6ff704ec11dd4a5f73d5b5df5721c4fee649527b
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 2%

---

# 管理環境 {#manage-your-environments}

>[!NOTE]
>要瞭解有關在as a Cloud Service中管理Cloud Manager環境的信AEM息，請參閱 [這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=en#using-cloud-manager)。

的 **概述** 雲管理器的頁面包括 **環境** 列出所有托管環境AEM的磁貼。

列出的每個環境都顯示其關聯狀態。

![](assets/Manage-Environ-Overview.png)

## 視頻教程 {#video-tutorial}

### Cloud Manager環境概述 {#environ-video}

以下視頻概述了由AEM作者、AEM發佈和Dispatcher實例組成的Cloud Manager環境。

>[!VIDEO](https://video.tv.adobe.com/v/26318/)

## 訪問雲管理器中的環境 {#accessing-environments-in-cloud-manager}

的 **環境** 磁貼顯示程式中預配的生產和舞台環境以及狀態。

狀態是環境中節點間的累計電源狀態。 如果所有節點都在運行，則呈綠色；如果一個節點停止，則呈紅色；如果一個節點出現，則呈藍色；如果一個節點的電源狀態不可用，則呈黃色（按優先順序順序）。

![](assets/Environments-card-new.png)

### 環境 {#environments}

按一下 **管理** 顯示 **環境** 的上界。

的 **環境** 螢幕顯示每張卡 *生產* 和 *舞台* （如果適用）。 每張卡上方都可以看到環境的名稱。 該卡包括環境中的節點表以及CPU的t恤尺寸、儲存器、區域和狀態。

>[!NOTE]
>
>的 **狀態** 節點的狀態表示VM的電源狀態，不反映伺服器AEM上的狀態。 狀態可以是 **正在運行** （綠色圓圈）, **已停止** （紅圓圈）, **快來** （藍色圓圈）或 **不可用** （黃色圓圈）。

![](assets/Environments-tab.png)

>[!NOTE]
>
>如果您需要您的環境日誌，可以通過您的客戶成功工程師請求這些日誌。
