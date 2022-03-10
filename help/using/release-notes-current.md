---
title: 2022.3.0 版發行說明
description: 這些是Cloud Manager 2022.3.0版的發行說明。
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: 0d14adda454889eebbb0a875978ceeaa5ee4f7ea
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 4%

---


# Cloud Manager版本2022.3.0的發行說明 {#release-notes}

此頁記錄的發行說明 [!UICONTROL Cloud Manager] 2022.3.0版。

>[!NOTE]
>
>有關as a Cloud Service中Cloud Manager的最新發AEM行說明，請參閱 [Cloud Manager(在AEMas a Cloud Service的當前發行說明中)。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## 發行日期 {#release-date}

發放日期 [!UICONTROL Cloud Manager] 2022.3.0版為2022年3月10日。 下一版計畫於2022年4月7日發行。

## 新增功能 {#what-is-new}

* (僅Cloud Service)訪AEM問「環境」日誌可以使用「開發人員」角色完成。
* 的 [`reliability_rating` 臨界度量](understand-your-test-results.md) 已禁用。


## 錯誤修正 {#bug-fixes}

* [的 **跳過負載平衡器更改** 選項](configuring-production-pipelines.md#adding-production-pipeline) 現在可以正確禁用。
* [的 **跳過負載平衡器更改** 選項](configuring-production-pipelines.md#adding-production-pipeline) 現在顯示編輯部署管道工作流。
* 手動建立的Git儲存庫的子集具有不正確的名稱值，這影響了 [生成項目重用功能。](setting-up-project.md#build-artifact-reuse) 這些資料庫的名稱已更改，用戶將在Cloud Manager API/UI中看到更正的名稱。
* [添加或編輯代碼質量管道時，](configuring-non-production-pipelines.md) 不再顯示處理度量故障的選項。
* 意外的管道變數配置不再導致生成步驟中的錯誤。
