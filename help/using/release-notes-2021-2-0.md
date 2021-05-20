---
title: 2021.2.0 版發行說明
seo-title: AEM Cloud Manager 2021.2.0版發行說明
description: 請詳閱本頁，了解Cloud Manager 2020.2.0版的相關資訊
seo-description: 請詳閱本頁，以取得AEM Cloud Manager 2021.2.0版的相關資訊
exl-id: 4f3c3a63-141b-414f-a24e-1870e985873a
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 4%

---

# 2021.2.0 版發行說明 {#release-notes-for}

以下章節概述[!UICONTROL Cloud Manager] 2021.2.0版的一般發行說明。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2021.2.0版的發行日期為2021年2月11日。

## 新功能 {#whats-new}

* 專案和沙箱建立中使用的AEM專案原型已更新為25版。

* 程式碼掃描期間識別的已棄用API清單已經過細化，加入最新Cloud ServiceSDK版本中已棄用的其他類別和方法。

* 生產部署現在可同時部署至配對的發佈與調度程式執行個體。

* 已更新Cloud Manager的SonarQube設定檔，以移除Sonar規則`squid:S2142`。 這不再與執行緒中斷檢查衝突。

* 以聲納為首碼的客戶`pom.xml`檔案中設定的屬性現在會動態移除，以避免建置和品質掃描失敗。

* 已新增其他程式碼品質規則，以涵蓋Cloud Service相容性問題。

## 錯誤修正 {#bug-fixes}

* 有時，CI/CD（部署）管道在效能測試步驟期間失敗，因為執行負載測試的容器發生錯誤。

* 有時，即使只發生一個例外，載入測試容器也會將執行報告為失敗。 只有在無法還原測試程式時，才會報告失敗。

* 儲存環境名稱的方式之間的某些機箱不匹配會導致效能測試失敗。

* 某些管道故障錯誤報告為管道錯誤。
