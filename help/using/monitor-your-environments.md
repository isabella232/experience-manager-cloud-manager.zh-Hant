---
title: 監控您的環境
seo-title: 監控您的環境
description: 'null'
seo-description: 請依照此頁面來瞭解Cloud Manager中的「系統監控」，方法是觀察環境中的個別執行個體，並追蹤每個執行個體的各種量度。
translation-type: tm+mt
source-git-commit: 1dfb065c09569f811e5a006d3d74825d3bd7cc8d

---


# 系統監控 {#system-monitoring}

系統監控方法 [!UICONTROL Cloud Manager] 是在環境中觀察個別執行個體，並追蹤每個執行個體的各種量度。每個度量都有兩個定義的臨界值- *警告臨界值* 和 *臨界臨界值*。

如果量度超過臨界臨界值，則被視為處於關鍵狀態；如果量度高於警告臨界值(但低於臨界值)，則會被視為警告狀態。臨界值由Adobe Managed Services設定，可以視覺化 [!UICONTROL Cloud Manager]。在大多數情況下，客戶之間的臨界值一致，但有時Adobe Managed Services會修改臨界值以符合特定客戶需求。有關臨界值的問題，應向客戶成功工程師(CSE)提出。

## 導覽至系統監控 {#navigating-system-monitoring}

導覽至「系統監控」功能可有兩種方式。

1. 登入 **受管理服務-程式** 著陸頁面。

   ![](assets/ProgramLanding.png)

1. 按一下程式卡片上的第三個圖示。

   ![](assets/program-card.png)

   *或*,

* 透過內建的全域導覽功能表項目，導覽至 **「系統監控****** 」著陸頁面 [!UICONTROL Cloud Manager]。


## 系統監控概述頁面 {#system-monitoring-overview-page}

「系統監控概述」頁面列出程式中受監控的環境，並報告其高階健康狀況的報告：

* **主機**
* **儲存**
* **網路**
* **應用程式**

每個類別中的狀態是個別度量的摘要-如果類別中的任何度量處於關鍵狀態，則整個類別都處於重要狀態，用於概述頁面。您可以在環境層級和執行個體層級檢視相同的摘要。

![](assets/Reports.png)

>[!NOTE]
>
>在導覽至此頁面時，會顯示生產環境例項，但也可以開啓其他環境。

## 系統監控詳細資訊 {#system-monitoring-detail}

若要檢視特定度量的詳細資訊，您可以按一下左側導覽中的其中一個類別，或按一下特定例項的其中一個類別指示符。每個詳細資料頁面會顯示該類別內度量的一系列圖表。您可以在環境或特定例項中檢視所有例項的度量。您可以使用右上角的下拉式方塊，在環境和例項之間切換。

![](assets/System_Monitoring1.png)

左側的導覽將顯示目前選取的類別中可用量度，其中包含目前所選環境和例項的資料。

![](assets/System_Monitoring2.png)

個別圖表會隨著時間顯示資料的狀態和圖表。如果顯示多個例項，則每個例項的資料將位於個別系列上。

![](assets/System-Monitoring3.png)

您可以按一下圖例中的系列，將個別系列隱藏在圖形上。
例如，如果您按一下警告臨界值系列，則只會看見臨界臨界值。

![](assets/System_Monitoring4.png)

### 度量定義 {#metric-definitions}

**主機**

* 每個核心載入：CPU或等待狀態在一個(載入1)、五個(載入5)和15(載入15)分鐘期間平均執行的程序數。
* 程序計數：目前開啓的程序數。
* 使用者計數：具有作用中殼層工作階段的使用者人數。
* 記憶體使用量：目前配置的系統記憶體百分比。
* JVM記憶體(堆積)：配置的Java Heap的大小(位於Megytes)。
* 舊世代空間：目前配置的JVM舊世代記憶體百分比。

**網路**

* CQ Port Check：存取AEM或Dispatcher連接埠的回應時間。作者、發佈和分派程式有不同的度量。

**儲存**

* 磁碟空間：主機上每個安裝點所使用的磁碟空間(位於Megytes)。每個掛載點都有不同的度量。您至少會看到「/」和「/mt」度量，但額外的掛載點量度可能會根據特定的例項設定提供。
* 資料夾大小：AEM區段商店：AEM區段商店適用的磁碟空間(位於Gigabyte)。

**應用程式**

* Replication Agent：測試複製事件的時間(單位為秒)。每個復本代理有不同的度量。
* Dispatcher刷新：dispatcher刷新佇列中目前的項目數。

## SLA報告 {#sla-reporting}

客戶可檢視其生產AEM環境相對於其合約服務層級合約(SLA)的績效。這可透過「報表」畫面上的子功能表取得。
例如，下圖顯示2018年的每月SLA精選。

![](assets/sla-reporting1.png)

與系統監控圖表一樣，滾動資料點會顯示該月的特定值。

![](assets/sla-reporting2.png)

此圖表下的「事件分析」區段顯示在目前選取年份內，程式發生的事件集。每個事件都有時間範圍、原因和一組注釋。

![](assets/sla-reporting3.png)

## SLA量度 {#sla-metrics}

* **作者合約**：這是您與Adobe Managed Services合約中針對作者層所定義的SLA。

* **AMS作者SLA**：這是由Adobe或我們供應商所造成生產作者層因子事件的測量運作時期。

* **作者SLA**：這是作者忽略已排程停機時間(例如維護視窗)的測量正常運作時間。

* **使用者合約**：這是您與Adobe Managed Services合約中針對發佈層所定義的SLA。

* **AMS終端使用者SLA**：這是生產上的測量運作時間，是由Adobe或我們的供應商所造成的。

* **用戶SLA**：這是發佈層忽略已排程停機時間(例如維護時段)的測量時段。