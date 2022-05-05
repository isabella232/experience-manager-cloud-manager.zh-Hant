---
title: 2022.5.0 版發行說明
description: 這些是Cloud Manager 2022.5.0版的發行說明。
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: 0ddfd152cb15731882d198d043dd8897b5073ab4
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 5%

---


# Cloud Manager版本2022.5.0的發行說明 {#release-notes}

此頁記錄的發行說明 [!UICONTROL Cloud Manager] 2022.5.0版。

>[!NOTE]
>
>有關as a Cloud Service中Cloud Manager的最新發AEM行說明，請參閱 [Cloud Manager(在AEMas a Cloud Service的當前發行說明中)。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## 發行日期 {#release-date}

發放日期 [!UICONTROL Cloud Manager] 2022.5.0版是2022年5月5日。 下一版計畫於2022年6月9日發行。

## 新增功能 {#what-is-new}

可以使AEM用開發人員角色訪問環境日誌。

## 錯誤修正 {#bug-fixes}

* 手動建立的Git儲存庫的子集具有不正確的名稱值，這防止了生成項目重用功能的有效性。 這些資料庫的名稱已更改，用戶將在Cloud Manager API/UI中看到更正的名稱。
* 來自非生產管道的生成工件在生產完整堆棧管道上被不恰當地重複使用。
* 添加或編輯代碼質量管道時，不再顯示處理度量失敗的選項。
* 某些意外的管道變數配置可能導致生成步驟中出現錯誤。
