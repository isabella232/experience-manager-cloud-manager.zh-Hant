---
title: 2022.9.0 版發行說明
description: 以下是Cloud Manager 2022.9.0版的發行說明。
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: e74d386d0b2d50a7e276bb7ead7594ef448742ae
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 4%

---


# Cloud Manager 2022.9.0版發行說明 {#release-notes}

本頁記錄 [!UICONTROL Cloud Manager] 版本2022.9.0。

>[!NOTE]
>
>如需AEM as a Cloud Service中Cloud Manager的最新發行說明，請參閱 [AEM Manager最新發行說明中。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## 發行日期 {#release-date}

的發行日期 [!UICONTROL Cloud Manager] 版本2022.9.0為2022年9月8日。 下一版預計於2022年10月6日發行。

## 新增功能 {#what-is-new}

* Cloud Manager支援水準多區域自動縮放。
* 新的「歡迎頁面」卡，針對只有Cloud Manager使用者角色的使用者而自訂，引導他們如何導覽至AEM環境及限制方案存取權。
* 沒有任何Cloud Manager角色的客戶將無法存取計畫詳細資訊。 不過，他們可從CM登陸頁面導覽至製作端點。
* 通過構建更強的可復原性，消除由重試失敗引起的管道故障。

## 錯誤修正 {#bug-fixes}

* 改善當maven遇到私人回購的連線問題時，與客戶AEM應用程式建置相關的客戶意見。
* 在少數情況下，當運行狀況檢查系統無法檢索有效的運行狀況分數時，將不會觸發自動縮放事件。
