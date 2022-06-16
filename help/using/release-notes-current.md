---
title: 2022.6.0 版發行說明
description: 這些是Cloud Manager 2022.6.0版的發行說明。
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: dab08a2499b521b7026ab2bd17b82cb241f26fb6
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 3%

---


# Cloud Manager版本2022.6.0的發行說明 {#release-notes}

此頁記錄的發行說明 [!UICONTROL Cloud Manager] 2022.6.0版。

>[!NOTE]
>
>有關as a Cloud Service中Cloud Manager的最新發AEM行說明，請參閱 [Cloud Manager(在AEMas a Cloud Service的當前發行說明中)。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## 發行日期 {#release-date}

發放日期 [!UICONTROL Cloud Manager] 2022.6.0版是2022年6月9日。 下一版計畫於2022年6月30日發行。

## 新增功能 {#what-is-new}

* Cloud Manager登錄頁上的新歡迎卡使用戶能夠快速訪問與租戶相關的入門教程和進度度量。
   * 此功能將在發佈後的一週內分階段2022.06.0出。
* [現在可以重用生成對象](/help/using/setting-up-project.md#build-artifact-reuse) 使用git鏡像時。

## API更改 {#api-changes}

* 的 [`List Programs`](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getPrograms) API已棄用， [`List Programs for Tenant`](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getProgramsForTenant) 應改為使用。
   * `List Programs` 繼續工作，但其使用將在日誌中生成警告消息。
   * 三個月後，它將不再得到支援。
