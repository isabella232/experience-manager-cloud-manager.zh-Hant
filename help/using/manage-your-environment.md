---
title: 管理您的環境
seo-title: 管理您的環境
description: 'null'
seo-description: 請依照本頁查看用於在Cloud manager中設定和運行CI/CD管道的生產和非生產環境的清單。
uuid: 04e67572-11db-4d5d-acf3-fd7f644a95f0
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: 使用
discoiquuid: c5b39de2-3a9b-437f-98e8-e6e6249a5b3a
translation-type: tm+mt
source-git-commit: dd23fc2277c2e2c51e3ab9b071d6336d2e0d6488

---


# 管理您的環境 {#manage-your-environments}

Cloud manager **的** 「概述」頁面包含「 **Environments** 」圖格，其中列出所有受管理的AEM環境。

每個列出的環境都顯示其關聯狀態。

![](assets/Manage_Environments1.png)

## 教學影片 {#video-tutorial}

### Cloud manager環境概述 {#environ-video}

以下影片提供由AEM Author、AEM Publish和Dispatcher例項組成的Cloud manager環境概觀。

>[!VIDEO](https://video.tv.adobe.com/v/26318/?captions=chi_hant)

## 在Cloud manager中訪問環境 {#accessing-environments-in-cloud-manager}

「環 **境** 」圖格會顯示您的程式中布建的「生產」和「舞台」環境以及狀態。

狀態是環境中節點上累計的電源狀態。 如果所有節點都在運行，則為綠色；如果某個節點停止，則為紅色；如果某個節點出現，則為藍色；如果某個節點的電源狀態不可用，則為黃色（按此優先順序順序）。

![](assets/manage_environments-screen2.png)

### 環境 {#environments}

按一 **下「管** 理」以顯示「 **環境** 」畫面。

「環 **境** 」畫面會針對您的程式中的 *Production* 和 *Stage* （如適用）環境顯示資訊卡。 每張卡片上方會顯示環境名稱。 該卡包括環境中的節點表，以及CPU的t恤大小、儲存、區域和狀態。

>[!NOTE]
>
>節 **點的STATUS** 代表VM的電源狀態，不反映伺服器上AEM的狀態。 狀態可以是「 **Running** (circle)」、「 **Stopped** （紅色圓圈）」、「Furing up **（藍色圓圈）」或「****** UnavailableCircle（黃色圓圈）」。

![](assets/Manage_Environments2.png)
