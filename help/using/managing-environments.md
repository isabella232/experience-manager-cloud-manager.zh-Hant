---
title: 管理環境
description: 了解如何使用 Cloud Manager 來管理您的環境。
exl-id: 700b0b4c-1e1a-4993-b366-426b14a98f8e
source-git-commit: 80f8707e00357f5a08dd835b846c9ee610f3e573
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 100%

---


# 管理環境 {#managing-environments}

了解如何使用 Cloud Manager 來管理您的環境。

## 總覽頁面 {#overview-page}

**Cloud Manager 的總覽**&#x200B;頁面包括&#x200B;**環境**&#x200B;圖磚，上面會提供所有受管理的 AEM 環境清單。

此環境清單中的每一項都會顯示其相關的狀態。

![總覽頁面](/help/assets/Manage-Environ-Overview.png)

## 環境圖磚 {#environments-tile}

此&#x200B;**環境**&#x200B;圖磚會顯示在您的方案中佈建的生產和中繼環境以及狀態。

此狀態指依據以下優先順序跨越環境中的節點彙總的電源狀態。

* 綠色 - 所有節點運作中
* 紅色 - 一或更多節點已停止。
* 藍色 - 一或更多節點將啟動。
* 黃色 - 一或更多節點無法提供電源狀態。

![環境圖磚](/help/assets/Environments-card-new.png)

## 管理環境 {#managing-environments-with-cloud-manager}

在&#x200B;**環境**&#x200B;圖磚上，按一下&#x200B;**管理**，即可顯示&#x200B;**環境**&#x200B;畫面。

此&#x200B;**環境**&#x200B;畫面會顯示各代表方案中的生產和中繼環境的卡片 (如適用)。每張卡片的上方都會顯示環境名稱。卡片會包括環境中的節點表以及 CPU 的 T 恤尺寸、儲存空間、區域和狀態。

>[!NOTE]
>
>節點的&#x200B;**狀態**&#x200B;並不表示 VM 的電源狀態，且不反映伺服器上 AEM 的狀態。該狀態有可能是：

* 綠色 - 運作中
* 紅色 - 已停止
* 藍色 - 即將啟動
* 黃色 - 無法提供

![「環境」索引標籤](/help/assets/Environments-tab.png)

>[!NOTE]
>
>如果您需要環境紀錄，可透過您的客戶成功工程師索取。

## 教學課程影片 {#video-tutorial}

此影片會提供對 Cloud Manager 環境的總覽，由 AEM 編寫、發佈以及 Dispatcher 執行個體組成。

>[!VIDEO](https://video.tv.adobe.com/v/26318/)
