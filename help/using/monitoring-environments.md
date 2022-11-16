---
title: 監視環境
description: 了解如何在 Cloud Manager 中監視環境。
exl-id: 32886133-d6c0-4aed-8bb0-81b84f63e825
source-git-commit: 5907ca6337d33c26ff19a14bfeb358cd9f7b935d
workflow-type: ht
source-wordcount: '939'
ht-degree: 100%

---


# 監視環境 {#monitoring-environments}

了解如何在 Cloud Manager 中監視環境。

## 量度臨界值 {#thresholds}

可透過觀察環境中的個別執行個體並追蹤每個執行個體的各種量度來完成 [!UICONTROL Cloud Manager] 中的系統監視。每個量度都有兩個已定義的臨界值：警告臨界值以及關鍵臨界值。

如果量度超越其關鍵臨界值，即被視為處於關鍵狀態。如果量度超越其警告臨界值 (但低於其關鍵臨界值)，即被視為處於警告狀態。此臨界值由 Adobe Managed Services 設定，並可在 [!UICONTROL Cloud Manager] 中視覺化。 在大多數情況下，客戶之間的臨界值會保持一致，但在某些情況下，Adobe Managed Services 會修改臨界值以和特定的客戶需求相符。如有關於臨界值的問題，應直接向您的客戶成功工程師 (CSE) 洽詢。

## 存取系統監視 {#accessing-system-monitoring}

請依照下列步驟存取系統監視。

1. 登入&#x200B;**Managed Services - 方案**&#x200B;登陸頁面。

   ![受管理服務的方案](/help/assets/ProgramLanding.png)

1. 按一下計劃卡上的第四個圖示。

   ![設定](/help/assets/first-timea1.png)


或者，您可以透過 [!UICONTROL Cloud Manager] 中的&#x200B;**報告**&#x200B;全域導覽選單項目瀏覽至&#x200B;**系統監視**&#x200B;登陸頁面。

## 系統監視概觀 {#system-monitoring-overview}

此系統監視概觀頁面會包含方案中受監視的環境清單，並報告四個不同類別中的高層級健康狀況：

* 主機
* 儲存空間
* 網路
* 應用程式

每個類別中的狀態是個別量度的摘要。如果某個類別中的任何量度處於關鍵狀態，則概觀頁面上的整個類別都會處於關鍵狀態。在環境層級和執行個體層級可檢視相同的摘要。

![系統監視概觀](/help/assets/System-Monitoring-Reports.png)

>[!NOTE]
>
>預設情況下，瀏覽至此頁面時，可看見生產環境執行個體，但也可檢視其他環境。

## 系統監視詳細資訊 {#system-monitoring-detail}

若要檢視特定量度的詳細資訊，您可以按一下左側導覽中的其中一個類別或按一下特定執行個體的其中一個類別指標。每個詳細資訊頁面都會顯示該類別中量度的一系列圖表。您可以檢視環境中所有執行個體或特定執行個體的量度。您可以使用右上角的下拉式方框在環境和執行個體之間進行切換。

![選取環境](/help/assets/System_Monitoring1.png)

左側的導覽將顯示目前所選類別中的可用量度，其中包含目前所選環境和執行個體的資料。

![監視量度](/help/assets/System_Monitoring2.png)

個別的圖表將顯示狀態和隨時間變化的資料圖表以及臨界值。如果顯示多個執行個體，則每個執行個體的資料將顯示在單獨的系列上。

![量度圖表](/help/assets/Monitoring_Graphs1.png)

按一下圖例中的系列，即可將圖表上的個別系列隱藏。
例如，如果您按一下警告臨界值系列，您將只能看到關鍵臨界值。

![修改圖表](/help/assets/Monitoring_Graphs2.png)

### 量度定義 {#metric-definitions}

#### 主機 {#host}

* **每個核心處理器的負載**：在一 (load1)、五 (load5) 和十五 (load15) 分鐘期間 CPU 正在執行或處於等候狀態的流程數的平均值
* **流程計數**：目前未完成的流程數
* **使用者計數**：具備有效殼層工作階段的使用者數量
* **記憶體用量**：目前已分配的系統記憶體的百分比
* **JVM 記憶體**：已分配的 Java 堆積的大小 (以兆位元組為單位)
* **舊世代空間**：目前已分配的 JVM 舊世代記憶體的百分比

#### 網路 {#network}

* **CQ 連接埠檢查**：存取 AEM 或 Dispatcher 連接埠的回應時間 (以秒為單位)
   * 對於作者、發佈和 Dispatcher，有不同的量度。

#### 儲存空間 {#storage}

* **磁碟空間**：主機上每個掛接點已使用的磁碟空間 (以兆位元組為單位)
   * 每個掛接點都有不同的量度。
   * 最起碼會有 `/` 和 `/mnt` 的量度，但如要更多掛接點量度，可能需視特定執行個體設定而定。
* **資料夾大小**
* **AEM 區段存放區**：AEM 區段存放區已使用的磁碟空間 (以十億位元組為單位)

#### 應用程式 {#application}

* **複寫代理程式**：測試複寫事件所需時間 (以秒為單位)
   * 每個複寫代理程式都有單獨的量度。
* **Dispatcher 排齊**：目前在 Dispatcher 排齊佇列中的項目數

## SLA 報告 {#sla-reporting}

客戶能夠查看其生產 AEM 環境相對於其簽訂的服務等級協議 (SLA) 的效能。這可透過&#x200B;**報告**&#x200B;畫面上的子選單取得。

下圖會顯示 2018 年每月的 SLA 實現情況。

![SLA 2018 圖表](/help/assets/SLA-Reports-one.png)

和系統監視圖一樣，將資料點翻轉會顯示該月的特定值。

![資料點翻轉](/help/assets/SLA-Reports-two.png)

在此圖表下的&#x200B;**事件分析**&#x200B;區段會顯示在目前選定年度期間該方案發生的事故組合。每個事故都有一個時間範圍、一個原因和一連串評論。

![事件分析](/help/assets/sla-reporting3.png)

## SLA 量度 {#sla-metrics}

* **作者合約**：這是您和 Adobe&#x200B; Managed Services 的合約中為作者層級定義的 SLA。
* **AMS 作者 SLA**：這是對於由 Adobe&#x200B; 或我們的廠商引起的生產作者層級分解事故測量到的運作時間。
* **作者 SLA**：這是對於作者層級測量到的運作時間，忽略已排程的停工期，例如維護期。
* **一般使用者合約**：這是您和 Adobe&#x200B; Managed Services 的合約中為發佈層級定義的 SLA。
* **AMS 一般使用者 SLA**：這是對於由 Adobe&#x200B; 或我們的廠商引起的生產發佈層級分解事故測量到的運作時間。
* **一般使用者 SLA**：這是對於發佈層級測量到的運作時間，忽略已排程的停工期，例如維護期。

## 教學課程影片 {#video-tutorial}

本影片提供了使用 Cloud Manager Reports 產生的圖表來檢視您的方案環境的概觀。

>[!VIDEO](https://video.tv.adobe.com/v/26315/)
