---
title: 監控您的環境
seo-title: 監控您的環境
description: 'null'
seo-description: 請依照本頁瞭解Cloud manager中的系統監控，方法是觀察環境中的個別執行個體，並追蹤每個執行個體的各種度量。
translation-type: tm+mt
source-git-commit: 519f43ff16e0474951f97798a8e070141e5c124b

---


# 系統監控 {#system-monitoring}

中的系統監 [!UICONTROL Cloud Manager] 控是通過觀察環境中的單個實例並跟蹤每個實例的各種度量來完成的。 每個度量都有兩個定義的臨界值 *-警告臨界值* ，以 *及嚴重臨界值*。

如果量度超過臨界值，則視為臨界狀態；如果量度超過其警告臨界值（但低於其嚴重臨界值），則會視為處於警告狀態。 臨界值由Adobe Managed services設定，可在中視覺化 [!UICONTROL Cloud Manager]。 在大多數情況下，客戶之間的臨界值是一致的，但有時Adobe Managed services會修改臨界值以符合特定客戶需求。 有關臨界值的問題應該提交給您的客戶成功工程師(CSE)。

## 導航到系統監視 {#navigating-system-monitoring}

導覽至「系統監視」功能可透過兩種方式完成。

1. 登錄到 **Managed Services —— 程式登錄頁** 。

   ![](assets/ProgramLanding.png)

1. 按一下程式卡上的第三個圖示。

   ![](assets/program-card.png)

   *或*,

* 導覽至「系 **統監控** 」著陸頁面，瀏覽 **Reports** global導覽功能表項目 [!UICONTROL Cloud Manager]。


## 「系統監視概述」頁 {#system-monitoring-overview-page}

「系統監視概述」頁列出了程式中受監控的環境，並報告了四個不同類別的高級別運行狀況：

* **主機**
* **儲存**
* **網路**
* **應用程式**

每個類別的狀態是個別度量的摘要——如果某個類別中的任何度量處於關鍵狀態，則整個類別在概述頁面中都處於關鍵狀態。 在環境級別和實例級別都可以查看相同的總結。

![](assets/Reports.png)

>[!NOTE]
>
>依預設，導覽至此頁面時，生產環境例項是可見的，但其他環境也可開啟。

## 概述視訊至報表 {#video-reports}

「Cloud Manager報表」透過一組圖表提供方案環境和AEM例項的檢視，這些圖表可報告並追蹤每個AEM例項的各種量度。
請參閱以下視訊以取得詳細資訊。

>[!VIDEO](https://video.tv.adobe.com/v/26315/?captions=chi_hant)

## 系統監控詳細資訊 {#system-monitoring-detail}

若要檢視特定度量的詳細資訊，您可以按一下左側導覽中的其中一個類別，或按一下特定例項的其中一個類別指標。 每個詳細資料頁面會顯示該類別中量度的一連串圖表。 您可以檢視環境中所有例項或特定例項的度量。 您可以使用右上角的下拉式方塊，在環境和例項之間切換。

![](assets/System_Monitoring1.png)

左側的導覽將顯示目前所選類別中的可用量度，目前所選環境和例項的資料都在此類別中。

![](assets/System_Monitoring2.png)

個別圖表會顯示一段時間內的資料狀態和圖表，以及臨界值。 如果顯示多個實例，則每個實例的資料將位於單獨的系列中。

![](assets/Monitoring_Graphs1.png)

按一下圖例中的系列，即可將個別系列隱藏在圖形上。
例如，如果您按一下警告臨界值系列，您只會看到嚴重臨界值。

![](assets/Monitoring_Graphs2.png)

### 量度定義 {#metric-definitions}

**主機**

* 每個核心的負載：由CPU執行或處於等待狀態的進程數平均在1(load1)、5(load5)和15(load15)分鐘期間內。
* 進程計數：當前開啟的進程數。
* 使用者計數：具有活動殼層會話的用戶數。
* 記憶體使用量：當前分配的系統記憶體的百分比。
* JVM記憶體（堆）:已分配Java堆的大小（以兆位元組為單位）。
* 老一代空間：當前分配的JVM舊代記憶體的百分比。

**網路**

* CQ埠檢查：存取AEM或Dispatcher埠的回應時間（以秒為單位）。 作者、發佈和分派程式有不同的度量。

**儲存**

* 磁碟空間：主機上每個裝載點的已用磁碟空間（以兆位元組為單位）。 每個裝載點有不同的度量。 至少，您會看到"/"和"/mnt"的量度，但是，其他的裝載點量度可能會視特定例項設定而定。
* 資料夾大小：AEM區段商店：AEM區段商店的已用磁碟空間（以GB為單位）。

**應用程式**

* 複製代理：測試複製事件的時間（以秒為單位）。 每個複製代理都有不同的度量。
* Dispatcher Flush:當前在調度器刷新隊列中的項目數。

## SLA報告 {#sla-reporting}

客戶可以看到其生產AEM環境相對於其合約服務層級合約(SLA)的效能。 這可透過「報表」畫面上的子功能表取得。
例如，下圖顯示2018年的月度SLA成績。

![](assets/sla-reporting1.png)

和系統監控圖表一樣，滾動資料點顯示該月的特定值。

![](assets/sla-reporting2.png)

此圖表下的「事件分析」區段顯示在目前選取年度內，程式發生的事件集。 每個事件都有一個時間範圍、一個原因和一組注釋。

![](assets/sla-reporting3.png)

## SLA度量 {#sla-metrics}

* **作者合約**:這是您與Adobe Managed services簽訂的作者層合約中定義的SLA。

* **AMS作者SLA**:這是由Adobe或我們的廠商造成的生產作者層級保理事件，經評估的持續運作時間。

* **作者SLA**:這是作者層所測量的正常運行時間，忽略計畫的停機時間（如維護窗口）。

* **使用者合約**:這是您與Adobe Managed services簽訂的發佈層合約中定義的SLA。

* **AMS最終用戶SLA**:這是由Adobe或我們的廠商所造成的生產發佈層代理事件，經評估的正常運作時間。

* **最終用戶SLA**:這是發佈層的測量正常運行時間，忽略計畫的停機時間（如維護窗口）。