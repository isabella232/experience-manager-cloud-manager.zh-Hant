---
title: 監視環境
description: 瞭解如何在雲管理器中監視您的環境。
exl-id: 32886133-d6c0-4aed-8bb0-81b84f63e825
source-git-commit: 5907ca6337d33c26ff19a14bfeb358cd9f7b935d
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---


# 監視環境 {#monitoring-environments}

瞭解如何在雲管理器中監視您的環境。

## 度量閾值 {#thresholds}

系統監視 [!UICONTROL Cloud Manager] 通過觀察環境中的單個實例並跟蹤每個實例的各種度量來完成。 每個度量都有兩個定義的閾值：警告閾值和嚴重閾值。

如果度量超過其臨界閾值，則它被視為處於臨界狀態。 如果度量超過其警告閾值（但低於其嚴重閾值），則它被視為處於警告狀態。 閾值由Adobe Managed Services設定，可在 [!UICONTROL Cloud Manager]。 在大多數情況下，客戶之間的閾值是一致的，但在某些情況下，Adobe Managed Services將修改閾值以滿足特定客戶要求。 有關閾值的問題應轉發給您的客戶成功工程師(CSE)。

## 訪問系統監視 {#accessing-system-monitoring}

按照以下步驟訪問「System Monitoring（系統監視）」。

1. 登錄到 **Managed Services — 方案** 登錄頁。

   ![托管服務程式](/help/assets/ProgramLanding.png)

1. 按一下程式卡上的第四個表徵圖。

   ![設定](/help/assets/first-timea1.png)


或者，您可以導航到 **系統監控** 登錄頁 **報告** 全局導航菜單項 [!UICONTROL Cloud Manager]。

## 系統監視概述 {#system-monitoring-overview}

「系統監視概述」頁列出了程式中受監視的環境，並報告了四個不同類別中的環境的高級運行狀況：

* 主機
* 儲存
* 網路
* 應用程式

每個類別的狀態是各個度量的摘要。 如果某個類別中的任何度量處於關鍵狀態，則整個類別在概述頁中處於關鍵狀態。 可以在環境級別和實例級別查看相同的總結。

![系統監視概述](/help/assets/System-Monitoring-Reports.png)

>[!NOTE]
>
>預設情況下，導航到此頁時，生產環境實例是可見的，但也可以查看其他環境。

## 系統監視詳細資訊 {#system-monitoring-detail}

要查看特定度量的詳細資訊，您可以按一下左導航中的一個類別，或按一下特定實例的一個類別指示符。 每個詳細資訊頁顯示該類別中度量的一系列圖形。 您可以查看環境中所有實例或特定實例的度量。 可以使用右上角的下拉框在環境和實例之間切換。

![選擇環境](/help/assets/System_Monitoring1.png)

左側的導航將顯示當前選定類別中的可用度量，當前選定環境和實例的資料都在此類別中。

![監視度量](/help/assets/System_Monitoring2.png)

單個圖表將顯示資料的狀態和隨時間變化的圖表以及閾值。 如果顯示多個實例，則每個實例的資料將位於單獨的系列中。

![度量圖](/help/assets/Monitoring_Graphs1.png)

通過按一下圖例中的系列，可以在圖形上隱藏單個系列。
例如，如果按一下警告閾值系列，則只會看到嚴重閾值。

![修改圖形](/help/assets/Monitoring_Graphs2.png)

### 度量定義 {#metric-definitions}

#### 主機 {#host}

* **每核負載**:CPU正在執行或處於等待狀態的進程數，在一(load1)、五(load5)和十五(load15)分鐘期間內平均
* **進程計數**:當前開啟的進程數
* **用戶計數**:具有活動Shell會話的用戶數
* **記憶體使用**:當前分配的系統記憶體百分比
* **JVM記憶體**:分配的Java堆的大小(MB)
* **舊一代空間**:當前分配的JVM舊代記憶體百分比

#### 網路 {#network}

* **CQ埠檢查**:訪問或Dispatcher埠的響應時間(以AEM秒為單位)
   * 作者、發佈和調度程式有不同的度量。

#### 儲存 {#storage}

* **磁碟空間**:主機上每個裝載點的已用磁碟空間(MB)
   * 每個裝載點有不同的度量。
   * 至少有 `/` 和 `/mnt`，但根據特定實例配置，可能有其他裝載點度量。
* **資料夾大小**
* **段AEM儲存**:段儲存的已用磁碟空間(千兆AEM位元組)

#### 應用程式 {#application}

* **複製代理**:test複製事件的時間（秒）
   * 每個複製代理都有單獨的度量。
* **調度程式刷新**:當前在調度程式刷新隊列中的項數

## SLA報告 {#sla-reporting}

客戶能夠看到其生產環境相對於AEM其合同服務級別協定(SLA)的效能。 此功能可通過 **報告** 的上界。

下圖顯示2018年的月度SLA成績。

![SLA 2018圖表](/help/assets/SLA-Reports-one.png)

與系統監視圖形一樣，滾動資料點顯示該月的特定值。

![資料點滾動](/help/assets/SLA-Reports-two.png)

的 **事件分析** 此圖表下的部分顯示當前選定年份中為程式發生的事件集。 每個事件都有一個時間範圍、一個原因和一組注釋。

![事件分析](/help/assets/sla-reporting3.png)

## SLA度量 {#sla-metrics}

* **作者合同**:這是您與Adobe Managed Services的合同中為作者層定義的SLA。
* **AMS作者SLA**:這是由Adobe或我們的供應商引起的生產作者層貼現事件的可測量正常運行時間。
* **作者SLA**:這是作者層所測量的正常運行時間，忽略計畫的停機時間（如維護窗口）。
* **最終用戶合同**:這是您與Adobe Managed Services的合同中為發佈層定義的SLA。
* **AMS最終用戶SLA**:這是由Adobe或我們的供應商引起的生產發佈層代理事件的計算正常運行時間。
* **最終用戶SLA**:這是發佈層所測量的正常運行時間，忽略計畫的停機時間（如維護窗口）。

## 視頻教程 {#video-tutorial}

此視頻提供並概述了如何使用Cloud Manager Reports生成的圖表來查看您的程式環境。

>[!VIDEO](https://video.tv.adobe.com/v/26315/)
