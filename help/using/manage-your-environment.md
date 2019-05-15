---
title: 管理您的環境
seo-title: 管理您的環境
description: 'null'
seo-description: 請依照此頁面檢視用於在Cloud Manager中設定及執行CI/CD管線的生產和非生產環境清單。
uuid: 04e67572-11db-4d5d-acf3-fd7 f644 a95 f0
contentOwner: jsyal
products: SG_ PERIENCENCENAGER/CLUDManager
topic-tags: 使用
discoiquuid: c5b39de2-3a9b-437f-98e8-e6 e6249 a5 b3 a
translation-type: tm+mt
source-git-commit: 1dfb065c09569f811e5a006d3d74825d3bd7cc8d

---


# 管理您的環境 {#manage-your-environments}

Cloud Manager的 **「概述** 」頁面包含 **「環境** 」方塊，可列出所有受管理的AEM環境。

每個列出的環境都會顯示其相關狀態。

![](assets/Manage_Environments1.png)

## 在Cloud Manager中存取環境 {#accessing-environments-in-cloud-manager}

**環境** 方塊會顯示程式中布建的Production and Stage環境以及狀態。

狀態是環境中節點間已捲動的電源狀態。如果所有節點都執行了綠色，則紅色是否會停止，如果某個節點已停止，則藍色是否為藍色，如果某個節點的電源狀態無法使用(依照此順序順序)，則為黃色。

![](assets/manage_environments-screen2.png)

### 環境 {#environments}

按一下 **「管理** 」以顯示 **「環境」** 畫面。

**「環境」** 畫面會在您的程式中顯示 *每個「生產」* 和 *「舞台」* 環境(適用)的卡片。每張卡片上會看到環境的名稱。卡片包含環境中的節點，以及CPU的t恤大小、儲存空間、地區和狀態。

>[!NOTE]
>
>節點 **的狀態** 代表VM的強大狀態，不反映伺服器上的AEM狀態。狀態可以是 **「執行(** 綠色圓圈)」、 **「已停止** 」(紅色圓圈)、「 **即將啓動」** (藍色圓形)或 **「無法使用** 」(黃色圓圈)。

![](assets/Manage_Environments2.png)
