---
title: 管理環境
description: 瞭解如何使用Cloud Manager管理您的環境。
exl-id: 700b0b4c-1e1a-4993-b366-426b14a98f8e
source-git-commit: 80f8707e00357f5a08dd835b846c9ee610f3e573
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 2%

---


# 管理環境 {#managing-environments}

瞭解如何使用Cloud Manager管理您的環境。

## 概覽頁 {#overview-page}

的 **概述** 雲管理器的頁面包括 **環境** 列出所有托管環境AEM的磁貼。

列出的每個環境都顯示其關聯狀態。

![概覽頁](/help/assets/Manage-Environ-Overview.png)

## 環境磁貼 {#environments-tile}

的 **環境** 磁貼顯示程式中預配的生產和暫存環境以及狀態。

狀態是按以下優先順序順序在環境中的節點上累計的電源狀態。

* 綠色 — 所有節點都在運行
* 紅色 — 停止一個或多個節點。
* 藍色 — 將出現一個或多個節點。
* 黃色 — 一個或多個節點的電源狀態不可用。

![環境磁貼](/help/assets/Environments-card-new.png)

## 管理環境 {#managing-environments-with-cloud-manager}

在 **環境** 平鋪，按一下 **管理** 顯示 **環境** 的上界。

的 **環境** 螢幕顯示程式中每個生產環境和登台環境（如果適用）的卡。 每張卡上方都可以看到環境的名稱。 該卡包括環境中的節點表以及CPU的t恤尺寸、儲存器、區域和狀態。

>[!NOTE]
>
>的 **狀態** 節點的狀態表示VM的電源狀態，不反映伺服器AEM上的狀態。 狀態可以是：

* 綠色 — 正在運行
* 紅色 — 已停止
* 藍色 — 即將出現
* 黃色 — 不可用

![「環境」頁籤](/help/assets/Environments-tab.png)

>[!NOTE]
>
>如果您需要您的環境日誌，可以通過您的客戶成功工程師請求這些日誌。

## 視頻教程 {#video-tutorial}

此視頻概括介紹了由創作、發佈和Dispatcher實例AEM組成的Cloud Manager環境。

>[!VIDEO](https://video.tv.adobe.com/v/26318/)
