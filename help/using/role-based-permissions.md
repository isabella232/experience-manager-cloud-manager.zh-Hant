---
title: 基於角色的權限
description: 請依照本頁來瞭解角色型權限。
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: introduction
discoiquuid: 67a54bae-99a9-4405-91e3-9a0a8b3ccc98
translation-type: tm+mt
source-git-commit: 157370b193c104915be063d1a4375f81839b88a2

---


# 基於角色的權限 {#role-based-permissions}

[!UICONTROL Cloud Manager] 具有具有適當權限的預先配置角色。 例如，開發人員會開發程式碼，並具有將程式碼推送至 **Git Repository的權限**。 或者，企業擁有者擁有不同的權限，可讓他們定義關鍵績效指標(KPI)並批准部署。

## 使用者角色 {#user-roles}

角色管理 [!UICONTROL Cloud Manager] 是在 [Adobe Admin Console中完成](https://helpx.adobe.com/enterprise/using/admin-console.html)。 任何使 [!UICONTROL Cloud Manager] 用者都必須是客戶IMS組織的成員，且具有Adobe Managed Services產品內容。 將使用者新增至「管理控制台」中的「產品設 [!UICONTROL Cloud Manager] 定檔」，以提供特定角色成員資格。

要瞭解有關如何設定角色的詳細資訊，請參 [閱設定用戶和角色](setting-up-users-and-roles.md)。

下表列出您可在管理控制台中指派的可能角色。

| **[!UICONTROL Cloud Manager]角色&#x200B;** | **說明** |
|---|---|
| 企業負責人 | 完成初始設定的主要 [!UICONTROL Cloud Manager] 使用者。 負責定義KPI、批准生產部署及覆寫重要的3層故障。 |
| 計畫經理 | 用於 [!UICONTROL Cloud Manager] 執行團隊設定、複查狀態和查看KPI。 可能會批准重要的3層故障。 |
| 部署管理員 | 管理部署操作。 用於 [!UICONTROL Cloud Manager] 執行階段和生產部署。 可能會批准重要的3層故障。 具有Git儲存庫的訪問權限。 |
| 開發人員 | 開發並測試自訂的應用程式碼。 主要用 [!UICONTROL Cloud Manager] 於查看狀態。 具有對Git儲存庫的提交訪問權。 |
| 客戶成功工程師 | 通常支援AMS客戶的成功。 為執行需 [!UICONTROL Cloud Manager] 要客戶成功工程師(CSE)監督的部署而與之互動。 |
| 內容作者 | 通常不與互動 [!UICONTROL Cloud Manager]。 此使用者可能會使 [!UICONTROL Cloud Manager] 用Program Switcher(已從 [!UICONTROL Experience Cloud])存取Adobe Experience Manager(AEM)。 |

## 使用者權限 {#user-permissions}

每個角色都具有與每個角色關聯的特定權限、預配置的任務或權限。 此表列出了可用的函式以及可以執行該函式的角色。

若要進一步瞭解如何設定您的使用者，請參閱 [設定使用者和角色](setting-up-users-and-roles.md)。

| 權限 | 說明 | 企業負責人 | 部署管理員 | 計畫經理 | 開發人員 | CSE |
|--- |--- |--- |--- |--- |--- |--- |
| 讀取應用程式 | 閱讀計畫KPI。 | x | x | x | x | x |
| 寫應用程式 | 程式設定或編輯。 | x |  |  |  |  |
| 添加程式 | 新增計畫。 | x |  |  |  |  |
| 閱讀環境 | 請參閱環境詳細資訊。 | x | x | x | x | x |
| 建立執行 | 啟動管線。 | x | x | x |  |  |
| 讀取執行 | 請參閱執行狀態。 | x | x | x | x | x |
| 繼續執行 | 可在暫停時繼續執行。 | x | x | x |  | x |
| 執行批准部署至生產 | 提供GoLive Approval。 | x | x | x |  |  |
| 執行計畫部署至生產 | 排程生產部署。 | x | x | x |  | x |
| 執行部署至生產 | 暫停CSE監督時，將應用程式部署至生產環境。 |  |  |  |  | x |
| 執行取消 | 取消當前執行。 | x | x | x |  |  |
| 執行覆蓋質量門失敗 | 批准重要的質量門故障。 | x | x | x |  |  |
| 管線建立 | 設定／編輯管線。 |  | x |  |  |  |
| 管線讀取 | 請參閱管線詳細資訊。 | x | x | x | x | x |
| 管線寫入 | 設定／編輯管線。 |  | x |  |  |  |
| 管線修改批准 | 允許編輯「業務所有者」選項。 |  | x |  |  |  |
| 管線修改受管部署 | 允許編輯CSE監督選項。 |  | x |  |  |  |
| 步驟讀取 | 請參閱步驟品質量度結果。 | x | x | x | x | x |
| 產生個人存取Token | 存取Git。 |  | x |  | x |  |

