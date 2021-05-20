---
title: 監控環境
seo-title: 監控環境
description: 了解如何在Cloud Manager中監控環境
seo-description: 請依照本頁所述，了解Cloud Manager中的系統監控，這是透過觀察環境中的個別例項並追蹤每個例項的各種量度來完成。
feature: 環境
exl-id: 32886133-d6c0-4aed-8bb0-81b84f63e825
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 1%

---

# 系統監視{#system-monitoring}

[!UICONTROL Cloud Manager]中的系統監控是透過觀察環境中的個別例項並追蹤每個例項的各種量度來完成。 每個度量有兩個定義的閾值 — *警告閾值*&#x200B;和&#x200B;*嚴重閾值*。

如果量度超過其臨界臨界值，則會視為處於臨界狀態；如果量度超過其警告臨界值（但低於其嚴重臨界值），則會視為處於警告狀態。 這些臨界值由Adobe Managed Services設定，並可在[!UICONTROL Cloud Manager]中視覺化。 在大多數情況下，客戶之間的臨界值是一致的，但在某些情況下，Adobe Managed Services會修改臨界值以符合特定客戶需求。 關於閾值的問題應指向您的客戶成功工程師(CSE)。

## 導航到系統監視{#navigating-system-monitoring}

導覽至「系統監控」功能可透過兩種方式完成。

1. 登入&#x200B;**Managed Services — 程式**&#x200B;登陸頁面。

   ![](assets/ProgramLanding.png)

1. 按一下程式卡上的第四個表徵圖。

   ![](assets/first-timea1.png)

   *或*,

* 通過[!UICONTROL Cloud Manager]內的&#x200B;**Reports**&#x200B;全局導航菜單項導航到&#x200B;**系統監視**&#x200B;登錄頁。


## 系統監視概述頁{#system-monitoring-overview-page}

「系統監視概述」頁列出了程式中受監視的環境，並報告了四個不同類別的高級運行狀況：

* **主機**
* **儲存**
* **網路**
* **應用程式**

每個類別的狀態是個別量度的摘要，如果類別中的任何量度處於關鍵狀態，則就概覽頁面而言，整個類別都處於關鍵狀態。 可在環境級別和實例級別查看相同的總結。

![](assets/System-Monitoring-Reports.png)

>[!NOTE]
>
>依預設，導覽至此頁面時，可看到生產環境例項，但也可以開啟其他環境。

## 影片教學課程{#video-tutorial}

### Cloud Manager報表概述{#reports-video}

Cloud Manager報表可透過一組圖表提供方案環境和AEM例項的檢視，以報告及追蹤每個AEM例項的各種量度。
如需詳細資訊，請參閱以下影片。

>[!VIDEO](https://video.tv.adobe.com/v/26315/)

## 系統監視詳細資訊{#system-monitoring-detail}

若要檢視特定量度的詳細資訊，您可以按一下左側導覽中的其中一個類別，或按一下特定例項的其中一個類別指標。 每個詳細資料頁面都會顯示該類別中量度的一系列圖形。 您可以檢視環境中所有例項或特定例項的量度。 您可以使用右上角的下拉式方塊，在環境和例項之間切換。

![](assets/System_Monitoring1.png)

左側的導覽會顯示目前所選類別中的可用量度，目前所選環境和例項的資料都在此類別中。

![](assets/System_Monitoring2.png)

個別圖表會顯示一段時間內的資料狀態和圖表，以及臨界值。 如果顯示多個例項，則每個例項的資料將位於不同的系列中。

![](assets/Monitoring_Graphs1.png)

按一下圖例中的系列，即可在圖形上隱藏個別系列。
例如，如果按一下警告閾值系列，則只會看到嚴重閾值。

![](assets/Monitoring_Graphs2.png)

### 量度定義{#metric-definitions}

**主機**

* 每個核心的載入：由CPU執行或處於等待狀態的進程數，在1(load1)、5(load5)和15(load15)分鐘週期內平均。
* 進程計數：當前開啟的進程數。
* 用戶計數：具有活動shell會話的用戶數。
* 記憶體使用率：當前分配的系統記憶體百分比。
* JVM記憶體（堆）:已分配Java堆的大小（以兆位元組為單位）。
* 老一代空間：當前分配的JVM舊代記憶體百分比。

**網路**

* CQ埠檢查：存取AEM或Dispatcher連接埠的回應時間（秒）。 製作、發佈和調度程式有不同的量度。

**儲存**

* 磁碟空間：主機上每個裝載點的已用磁碟空間（以兆位元組為單位）。 每個裝載點有不同的度量。 您至少會看到「/」和「/mnt」的量度，但視特定執行個體設定而定，可能會提供其他裝載點量度。
* 資料夾大小：AEM區段商店：AEM Segment Store的已用磁碟空間（以GB為單位）。

**應用程式**

* 複製代理：測試復寫事件的時間（以秒為單位）。 每個復寫代理都有不同的量度。
* Dispatcher排清：Dispatcher排清佇列中目前的項目數。

## SLA報告{#sla-reporting}

客戶能夠看到其生產AEM環境相對於其合同的服務級別協定(SLA)的效能。 這可透過「報表」畫面上的子功能表使用。
例如，下圖顯示2018年的月度SLA達到情況。

![](assets/SLA-Reports-one.png)

如同系統監控圖表一樣，滾動資料點會顯示該月的特定值。

![](assets/SLA-Reports-two.png)

此圖形下的「事件分析」部分顯示當前選定年度內為程式發生的事件集。 每個事件都有一個時間範圍、一個原因和一個注釋集。

![](assets/sla-reporting3.png)

## SLA度量{#sla-metrics}

* **作者合約**:這是您與Adobe Managed Services合約中針對作者階層所定義的SLA。

* **AMS作者SLA**:這是由Adobe或我們的供應商造成的生產製作層級保理事件的正常運行時間。

* **作者SLA**:這是作者層級所測量的正常運作時間，會忽略已排程的停機時間（例如維護期間）。

* **最終用戶合同**:這是您與Adobe Managed Services之合約中針對發佈層級所定義的SLA。

* **AMS一般使用者SLA**:這是由Adobe或我們的供應商造成的生產發佈層級保理事件的正常運行時間。

* **最終用戶SLA**:這是發佈層級測量的正常運作時間，會忽略已排程的停機時間（例如維護視窗）。
