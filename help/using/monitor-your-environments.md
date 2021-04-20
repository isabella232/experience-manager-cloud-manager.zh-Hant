---
title: 監控環境
seo-title: 監控環境
description: 瞭解如何在Cloud Manager中監控您的環境
seo-description: 請依照本頁瞭解Cloud Manager中的系統監控，方法是觀察環境中的個別執行個體，並追蹤每個執行個體的各種度量。
feature: Environments
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 1%

---


# 系統監視{#system-monitoring}

[!UICONTROL Cloud Manager]中的系統監控是通過觀察環境中的單個實例並跟蹤每個實例的各種度量來完成的。 每個度量有兩個定義的閾值- *警告閾值*&#x200B;和&#x200B;*嚴重閾值*。

如果量度超過臨界值，則視為臨界狀態；如果量度超過其警告臨界值（但低於其嚴重臨界值），則會視為處於警告狀態。 臨界值由Adobe Managed Services設定，可在[!UICONTROL Cloud Manager]中視覺化。 在大多數情況下，客戶之間的臨界值是一致的，但有時Adobe Managed Services會修改臨界值以符合特定客戶需求。 有關臨界值的問題應該提交給您的客戶成功工程師(CSE)。

## 導航到系統監視{#navigating-system-monitoring}

導覽至「系統監視」功能可透過兩種方式完成。

1. 登入&#x200B;**Managed Services-程式**&#x200B;登陸頁面。

   ![](assets/ProgramLanding.png)

1. 按一下程式卡上的第四個圖示。

   ![](assets/first-timea1.png)

   *或*,

* 導覽至&#x200B;**系統監控**&#x200B;登陸頁面，瀏覽[!UICONTROL Cloud Manager]內的&#x200B;**報告**&#x200B;全域導覽功能表項目。


## 「系統監視概述」頁{#system-monitoring-overview-page}

「系統監視概述」頁列出了程式中受監控的環境，並報告了四個不同類別的高級別運行狀況：

* **主機**
* **儲存**
* **網路**
* **應用程式**

每個類別的狀態是個別度量的摘要——如果某個類別中的任何度量處於關鍵狀態，則整個類別在概述頁面中都處於關鍵狀態。 在環境級別和實例級別都可以查看相同的總結。

![](assets/System-Monitoring-Reports.png)

>[!NOTE]
>
>依預設，導覽至此頁面時，生產環境例項是可見的，但其他環境也可開啟。

## 教學影片{#video-tutorial}

### Cloud Manager報告概述{#reports-video}

「雲端管理員報表」透過一組圖表提供方案AEM環境與例項的檢視，這些圖表會報告並追蹤每個例項的各種度AEM量。
請參閱以下視訊以取得詳細資訊。

>[!VIDEO](https://video.tv.adobe.com/v/26315/)

## 系統監視詳細資訊{#system-monitoring-detail}

若要檢視特定度量的詳細資訊，您可以按一下左側導覽中的其中一個類別，或按一下特定例項的其中一個類別指標。 每個詳細資料頁面會顯示該類別中量度的一連串圖表。 您可以檢視環境中所有例項或特定例項的度量。 您可以使用右上角的下拉式方塊，在環境和例項之間切換。

![](assets/System_Monitoring1.png)

左側的導覽將顯示目前所選類別中的可用量度，目前所選環境和例項的資料都在此類別中。

![](assets/System_Monitoring2.png)

個別圖表會顯示一段時間內的資料狀態和圖表，以及臨界值。 如果顯示多個實例，則每個實例的資料將位於單獨的系列中。

![](assets/Monitoring_Graphs1.png)

按一下圖例中的系列，即可將個別系列隱藏在圖形上。
例如，如果您按一下警告臨界值系列，您只會看到嚴重臨界值。

![](assets/Monitoring_Graphs2.png)

### 量度定義{#metric-definitions}

**主機**

* 每個核心的負載：由CPU執行或處於等待狀態的進程數平均在1(load1)、5(load5)和15(load15)分鐘期間內。
* 進程計數：當前開啟的進程數。
* 使用者計數：具有活動殼層會話的用戶數。
* 記憶體使用量：當前分配的系統記憶體的百分比。
* JVM記憶體（堆）:已分配Java堆的大小（以兆位元組為單位）。
* 老一代空間：當前分配的JVM舊代記憶體的百分比。

**網路**

* CQ埠檢查：訪問或Dispatcher埠的響應時間(以秒為AEM單位)。 作者、發佈和分派程式有不同的度量。

**儲存**

* 磁碟空間：主機上每個裝載點的已用磁碟空間（以兆位元組為單位）。 每個裝載點有不同的度量。 至少，您會看到&quot;/&quot;和&quot;/mnt&quot;的量度，但是，其他的裝載點量度可能會視特定例項設定而定。
* 資料夾大小：區AEM段商店：區段儲存區的已用磁碟空間(以吉AEM位元組為單位)。

**應用程式**

* 複製代理：測試複製事件的時間（以秒為單位）。 每個複製代理都有不同的度量。
* Dispatcher Flush:當前在調度器刷新隊列中的項目數。

## SLA報告{#sla-reporting}

客戶可以看到其生產環境相對於其合AEM同的服務級別協定(SLA)的效能。 這可透過「報表」畫面上的子功能表取得。
例如，下圖顯示2018年的月度SLA成績。

![](assets/SLA-Reports-one.png)

和系統監控圖表一樣，滾動資料點顯示該月的特定值。

![](assets/SLA-Reports-two.png)

此圖表下的「事件分析」區段顯示在目前選取年度內，程式發生的事件集。 每個事件都有一個時間範圍、一個原因和一組注釋。

![](assets/sla-reporting3.png)

## SLA度量{#sla-metrics}

* **作者合約**:這是您與Adobe Managed Services簽訂的作者層合約中定義的SLA。

* **AMS作者SLA**:這是由Adobe或我們的供應商造成的生產作者層級保理事件的衡量正常運行時間。

* **作者SLA**:這是作者層所測量的正常運行時間，忽略計畫的停機時間（如維護窗口）。

* **使用者合約**:這是您與Adobe Managed Services簽訂的發佈層合約中定義的SLA。

* **AMS最終用戶SLA**:這是由Adobe或我們的廠商所造成的生產發佈層代理事件的測量正常運行時間。

* **最終用戶SLA**:這是發佈層的測量正常運行時間，忽略計畫的停機時間（如維護窗口）。