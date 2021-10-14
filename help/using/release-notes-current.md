---
title: 2021.10.0 版發行說明
description: 請詳閱本頁以取得Cloud Manager版本2021.10.0的資訊
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: b28f8f1bedb92428d332716510cbf0fd714fada6
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 3%

---

# 2021.10.0 版發行說明 {#release-notes-for}

以下章節概述[!UICONTROL Cloud Manager] 2021.10.0版的一般發行說明。

>[!NOTE]
>請參閱[最新發行說明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/release-notes-cloud-manager/release-notes-cm-current.html?lang=en#getting-access) ，以在AEMas a Cloud Service中查看Cloud Manager的最新發行說明。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2021.10.0版的發行日期為2021年10月14日。
下一版預計於2021年11月4日發行。

## 新增功能 {#whats-new}

* 生產管道現在可以以「緊急」模式執行，略過緊急部署的安全性和效能測試步驟。

* 為與Cloud Service保持一致，現在UI中會參照現有部署管道，並將其標示為「完整堆疊」管道。

* 管道卡已重新整理，現在會顯示顯示生產管道和非生產管道的單一整合面板，且使用者可從與每個管道相關聯的動作功能表中直接選取「執行/暫停/繼續」。

* 部署管理員角色中的使用者現在可以透過UI以自助方式刪除生產管道。

* 新增和編輯管道體驗已重新整理，現在可使用熟悉的現代模組。

* Cloud Manager的使用者現在可以透過登錄頁面右上角的&#x200B;**Feedback**&#x200B;按鈕，直接從UI提交意見。

* 每年的SLA圖表現在可以從Cloud Manager使用者介面下載。

* 程式碼品質和非生產管道執行現在會在建置步驟期間使用更有效率的淺層復製程式，為擁有特別大型Git存放庫的客戶提供更快的建置時間。

* Cloud Manager API檔案現在包含互動式操作場，可讓登入的使用者透過瀏覽器試驗API。 如需詳細資訊，請參閱[Cloud Manager API Plearty](https://www.adobe.io/experience-cloud/cloud-manager/reference/playground/) 。

* 如果禁用「導航到」下的選擇選項，則「程式」卡上的工具提示將更具描述性。 現在會指出「生產環境不存在」。


## 錯誤修正 {#bug-fixes}

* 從內部系統讀取的資料未正確輸入時，可能導致CSE提供的不相關資料無法在Cloud Manager中正確反映。

* 在特定客戶情況下，建置步驟期間下載的無效成品（原本應導致建置失敗）會被忽略。
