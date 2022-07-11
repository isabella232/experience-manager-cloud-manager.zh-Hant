---
title: 以角色為主的權限
description: 瞭解Cloud Manager預先配置的基於角色的權限，以管理對雲資源的訪問。
exl-id: b66533fb-db93-40e8-919d-581261fdbf24
source-git-commit: 522e5fbc650a8159602eb1aeaf42d64f4e23e8b4
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 13%

---


# 角色型權限 {#role-based-permissions}

[!UICONTROL Cloud Manager] 具有預配置的具有適當權限的角色。 例如，開發人員開發代碼並有權將代碼推送到Git儲存庫。 業務所有者具有不同的權限，允許他們定義關鍵績效指標(KPI)並審批部署。

## 使用者角色 {#user-roles}

角色管理 [!UICONTROL Cloud Manager] 使用 [Admin Console。](https://helpx.adobe.com/enterprise/using/admin-console.html) 任何用戶 [!UICONTROL Cloud Manager] 必須是客戶IMS組織的成員，並且具有Adobe托管服務產品上下文。 通過將用戶添加到 [!UICONTROL Cloud Manager] 產品配置檔案。

要瞭解有關如何設定角色的詳細資訊，請參閱文檔 [設定用戶和角色。](/help/requirements/users-and-roles.md)

此表列出了可以在Admin Console中分配的角色。

| [!UICONTROL Cloud Manager] 角色 | 說明 |
|---|---|
| 業務所有者 | 這是完成初始操作的主要用戶 [!UICONTROL Cloud Manager] 設定並負責定義KPI、審批生產部署，以及在必要時改寫重要的3層故障。 |
| 程式管理器 | 此用戶使用 [!UICONTROL Cloud Manager] 要執行團隊設定、複查狀態、查看KPI，並在需要時可能審批重要的3層故障。 |
| 部署管理器 | 此用戶使用 [!UICONTROL Cloud Manager] 要執行階段和生產部署，可能會在必要時批准重要的3層故障，並有權訪問git儲存庫。 |
| 開發人員 | 此用戶開發和test自定義應用程式碼，主要使用 [!UICONTROL Cloud Manager] 查看部署狀態，並具有對git儲存庫的提交訪問權限。 |
| 客戶成功工程師 | 此用戶通常支援AMS客戶的客戶成功，並與 [!UICONTROL Cloud Manager] 執行需要客戶成功工程師(CSE)監督的部署。 |
| 內容作者 | 此用戶通常不與 [!UICONTROL Cloud Manager]，但可以使用 [!UICONTROL Cloud Manager] 程式witcher(從 [!UICONTROL Experience Cloud])訪問Adobe Experience Manager(AEM)。 |

## 使用者權限 {#user-permissions}

每個角色都具有特定的關聯預配置權限。 此表列出了可用的權限以及可以執行這些權限的角色。


| 權限 | 說明 | 業務所有者 | 部署管理器 | 程式管理器 | 開發人員 | CSE |
|--- |--- |--- |--- |--- |--- |--- |
| 讀取應用程式 | 讀取程式KPI | x | x | x | x | x |
| 寫入應用程式 | 程式設定或編輯 | x |  |  |  |  |
| 添加程式 | 添加新程式 | x |  |  |  |  |
| 讀取環境 | 查看環境詳細資訊 | x | x | x | x | x |
| 建立執行 | 啟動管線 | x | x | x |  |  |
| 讀取執行 | 請參閱執行狀態 | x | x | x | x | x |
| 恢復執行 | 可以在暫停時繼續執行 | x | x | x |  | x |
| 執行批准部署到生產 | 提供上線批准 | x | x | x |  |  |
| 執行計畫部署到生產 | 計畫生產部署 | x | x | x |  | x |
| 執行部署到生產 | 暫停CSE監督時將應用程式部署到生產 |  |  |  |  | x |
| 執行取消 | 取消當前執行 |  |  | x |  |  |
| 執行覆蓋質量門失敗 | 批准重要的質量門故障 | x | x | x |  |  |
| 管線建立 | 設定/編輯管線 |  | x |  |  |  |
| 管道讀取 | 請參閱管道詳細資訊 | x | x | x | x | x |
| 管道寫入 | 設定/編輯管線。 |  | x |  |  |  |
| 管道修改批准 | 允許編輯「業務所有者」選項 |  | x |  |  |  |
| 管道修改托管部署 | 允許編輯CSE監督選項 |  | x |  |  |  |
| 管道刪除 | 允許管道刪除 |  | x |  |  |  |
| 步驟讀取 | 請參閱步驟質量度量結果 | x | x | x | x | x |
| 生成個人訪問令牌 | 訪問Git |  | x |  | x |  |

要瞭解有關如何設定用戶查看文檔的詳細資訊 [設定用戶和角色。](/help/requirements/users-and-roles.md)
