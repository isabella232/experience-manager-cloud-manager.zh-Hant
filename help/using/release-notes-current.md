---
title: 2021.2.0 版發行說明
seo-title: AEM Cloud Manager 2021.2.0版本注意事項
description: 請依照本頁取得Cloud Manager 2021.2.0版的相關資訊
seo-description: 請依照本頁取得AEM Cloud Manager 2021.2.0版的相關資訊
translation-type: tm+mt
source-git-commit: 67cdd39cb511763a42391c7896924a1433e4e58f
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 5%

---

# 2021.2.0 版發行說明 {#release-notes-for}

下節概述[!UICONTROL Cloud Manager] 2021.2.0版的一般發行說明。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2021.2.0版的發行日期為2021年2月11日。

## 新功能 {#whats-new}

* 「專案與沙盒建立」中使用的AEM專案原型已更新為版本25。

* 程式碼掃描期間識別的已過時API清單已改良，加入最新Cloud Service SDK版本中已淘汰的其他類別和方法。

* 生產部署現在可並行部署至配對的發佈與分派器例項。

* SonarQube的Cloud Manager設定檔已更新，以移除Sonar規則`squid:S2142`。 這不會再與線程中斷檢查衝突。

* 現在，客戶`pom.xml`檔案中預先設定的Sonar屬性將會動態移除，以避免建置和品質掃描失敗。

## 錯誤修正 {#bug-fixes}

* 有時，CI/CD（部署）管線在效能測試步驟期間失敗，原因是執行負載測試的容器遇到錯誤。

* 有時，即使只發生一個例外情況，載入測試容器仍會將執行報告為失敗。 只有在無法還原測試程式時才會報告失敗。

* 儲存環境名稱的方式之間的某些機箱不匹配會導致效能測試失敗。

* 某些管線故障錯誤報告為管線錯誤。