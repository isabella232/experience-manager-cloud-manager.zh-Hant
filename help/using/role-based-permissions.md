---
title: 角色型權限
description: 請詳閱本頁面，了解角色型權限。
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: introduction
discoiquuid: 67a54bae-99a9-4405-91e3-9a0a8b3ccc98
feature: 使用者角色
exl-id: b66533fb-db93-40e8-919d-581261fdbf24
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 17%

---

# 角色型權限 {#role-based-permissions}

[!UICONTROL Cloud Manager] 已預先設定具有適當權限的角色。例如，開發人員開發程式碼，並擁有將程式碼推送至&#x200B;**Git存放庫**&#x200B;的權限。 或者，企業擁有者擁有不同的權限，可讓他們定義關鍵績效指標(KPI)並核准部署。

## 使用者角色 {#user-roles}

[!UICONTROL Cloud Manager]的角色管理是在[Adobe Admin Console](https://helpx.adobe.com/tw/enterprise/using/admin-console.html)內完成。 [!UICONTROL Cloud Manager]的任何使用者必須是客戶IMS組織的成員，且具備Adobe Managed Services產品內容。 將使用者新增至Admin Console的[!UICONTROL Cloud Manager]產品設定檔，以提供特定角色成員資格。

若要進一步了解如何設定您的角色，請參閱[設定使用者和角色](setting-up-users-and-roles.md)。

下表清單定義了可在Admin Console中分配的可能角色。

| **[!UICONTROL Cloud Manager]角色** | **說明** |
|---|---|
| 業務負責人 | 完成初始[!UICONTROL Cloud Manager]設定的主要用戶。 負責定義KPI、核准生產部署，以及覆寫重要的3層故障。 |
| 計畫經理 | 使用[!UICONTROL Cloud Manager]執行團隊設定、查看狀態和查看KPI。 可能批准重要的3層故障。 |
| 部署管理員 | 管理部署操作。 使用[!UICONTROL Cloud Manager]執行預備和生產部署。 可能批准重要的3層故障。 可存取Git存放庫。 |
| 開發人員 | 開發和測試自訂應用程式程式碼。 主要使用[!UICONTROL Cloud Manager]來檢視狀態。 已提交Git存放庫的存取權。 |
| 客戶成功工程師 | 通常支援AMS客戶的客戶成功。 與[!UICONTROL Cloud Manager]互動，以執行需要客戶成功工程師(CSE)監督的部署。 |
| 內容作者 | 通常不會與[!UICONTROL Cloud Manager]互動。 此使用者可使用[!UICONTROL Cloud Manager] Program Switcher（已從[!UICONTROL Experience Cloud]導覽）存取Adobe Experience Manager(AEM)。 |

## 使用者權限 {#user-permissions}

各角色皆擁有各自相關的特定權限、預設任務或權限。此表列出了可用函式以及可執行該函式的角色。

若要進一步了解如何設定您的使用者，請參閱[設定使用者和角色](setting-up-users-and-roles.md)。

| 權限 | 說明 | 業務負責人 | 部署管理員 | 計畫經理 | 開發人員 | CSE |
|--- |--- |--- |--- |--- |--- |--- |
| 讀取應用程式 | 閱讀方案KPI。 | x | x | x | x | x |
| 寫應用程式 | 程式設定或編輯。 | x |  |  |  |  |
| 添加程式 | 添加新程式。 | x |  |  |  |  |
| 讀取環境 | 請參閱環境詳細資訊。 | x | x | x | x | x |
| 建立執行 | 啟動管道。 | x | x | x |  |  |
| 讀取執行 | 請參閱執行狀態。 | x | x | x | x | x |
| 繼續執行 | 可在暫停時繼續執行。 | x | x | x |  | x |
| 執行批准部署到生產環境 | 提供GoLive核准。 | x | x | x |  |  |
| 執行計畫部署到生產環境 | 排程生產部署。 | x | x | x |  | x |
| 執行部署到生產環境 | 暫停CSE監督時，將應用程式部署到生產環境。 |  |  |  |  | x |
| 執行取消 | 取消當前執行。 |  |  | x |  |  |
| 執行覆蓋質量門失敗 | 批准重要的質量門故障。 | x | x | x |  |  |
| 管線建立 | 設定/編輯管道。 |  | x |  |  |  |
| 管道讀取 | 請參閱管道詳細資訊。 | x | x | x | x | x |
| 管道寫入 | 設定/編輯管道。 |  | x |  |  |  |
| 管道修改批准 | 允許編輯「業務所有者」選項。 |  | x |  |  |  |
| 管道修改托管部署 | 允許編輯CSE監督選項。 |  | x |  |  |  |
| 管道刪除 | 允許刪除管道。 |  | x |  |  |  |
| 步驟讀取 | 請參閱步驟品質量度結果。 | x | x | x | x | x |
| 產生個人存取權杖 | 存取Git。 |  | x |  | x |  |
