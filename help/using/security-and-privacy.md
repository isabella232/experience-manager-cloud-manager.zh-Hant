---
title: 安全性與隱私權
seo-title: AEM Cloud Manager的安全性與隱私權
description: 請依照本頁瞭解資產的安全性與隱私權(程式碼/人工消息)。
seo-description: 請依照本頁面，使用AEM Cloud Manager瞭解資產的安全性和隱私權(程式碼/路徑)。
uuid: 68bc2330-a62 c-4c2 c-925c-daha6488 b143 a
contentOwner: jsyal
products: SG_ PERIENCENCENAGER/CLUDManager
topic-tags: 簡介
discoiquuid: 67a54bae-99a9-4405-91e3-9a0a0b3cc98
translation-type: tm+mt
source-git-commit: 1dfb065c09569f811e5a006d3d74825d3bd7cc8d

---


# 安全性與隱私權 {#security-and-privacy}

[!UICONTROL Cloud Manager] 具有適當權限的預先設定角色。例如，開發人員開發程式碼，並擁有將程式碼推送至 **Git存放庫**的權限。或者，商業擁有者擁有不同權限，可定義關鍵績效指標(KPI)並核准部署。

## 角色型權限 {#role-based-permissions}

### 使用者角色 {#user-roles}

角色管理是在Adobe [!UICONTROL Cloud Manager] Admin [Console中完成](https://helpx.adobe.com/enterprise/using/admin-console.html)的。任何使用者都 [!UICONTROL Cloud Manager] 必須是客戶IMS組織的成員，並且擁有Adobe Managed Services產品上下文。您可以在Admin Console中新增使用者至 [!UICONTROL Cloud Manager] 產品描述檔，以提供特定角色會籍。

若要進一步瞭解如何設定角色，請參閱 [設定使用者和角色](setting-up-users-and-roles.md)。

下表列出您可以在「管理控制台」中指派的可能角色。

| **[!UICONTROL Cloud Manager]角色** | **說明** |
|---|---|
| 企業負責人 | 完成初始 [!UICONTROL Cloud Manager] 設定的主要使用者。負責定義KPI、核准生產部署並覆寫重要的層失敗。 |
| 方案經理 | 用於 [!UICONTROL Cloud Manager] 執行團隊設定、檢閱狀態及檢視KPI。可核准重要的層失敗。 |
| 部署管理員 | 管理部署作業。用於 [!UICONTROL Cloud Manager] 執行階段和生產部署。可核准重要的層失敗。擁有Git儲存庫的存取權。 |
| 開發人員 | 開發並測試自訂應用程式代碼。主要用於 [!UICONTROL Cloud Manager] 檢視狀態。已提交Git存放庫的權限。 |
| 客戶成功工程師 | 一般支援AMS客戶成功案例。與執行 [!UICONTROL Cloud Manager] 需要客戶成功工程師(CSE)監督的部署互動。 |
| 內容作者 | 通常不會與您互動 [!UICONTROL Cloud Manager]。此使用者可使用 [!UICONTROL Cloud Manager] Program Switcher(導覽自 [!UICONTROL Experience Cloud])存取Adobe Experience Manager(AEM)。 |

### 使用者權限 {#user-permissions}

每個角色都具有與每個角色相關的特定權限、預先設定的任務或權限。此表格列出可用的函數以及可執行函數的角色。

若要進一步瞭解如何設定使用者，請參閱 [設定使用者和角色](setting-up-users-and-roles.md)。

| 權限 | 說明 | 企業負責人 | 部署管理員 | 方案經理 | 開發人員 | CSE |
|--- |--- |--- |--- |--- |--- |--- |
| 閱讀應用程式 | 請參閱方案詳細資訊。 | x | x | x | x | x |
| 編寫應用程式 | 配置程式(包括KPI)。 | x |
| 閱讀環境 | 請參閱環境詳細資訊。 | x | x | x | x | x |
| 建立執行 | 開始管道。 | x | x | x |
| 閱讀執行 | 請參閱執行狀態。 | x | x | x | x | x |
| 繼續執行 | 暫停時可以繼續執行。 | x | x | x | x |
| 執行批准部署至生產 | 提供GoLive核准。 | x | x | x |
| 執行計劃部署至生產 | 排程生產部署。 | x | x | x | x |
| 執行部署至生產 | 暫停時將應用程式部署至生產環境。 | x |
| 執行取消 | 取消目前的執行。 | x | x | x |
| 執行覆蓋品質關卡失敗 | 核准重要品質關卡失敗。 | x | x | x |
| 管線建立 | 設定/編輯管道。 | x |
| 管道讀取 | 請參閱管道詳細資訊。 | x | x | x | x | x |
| 管線寫入 | 設定/編輯管道。 | x |
| 管道修改批准 | 允許編輯「商業擁有者」選項。 | x |
| 管線修改受管理部署 | 允許編輯「CSE監督」選項。 | x |
| 解決方案讀取 | 閱讀方案KPI。 | x | x | x | x | x |
| 解決方案寫入 | 設定程式(包括KPI)設定/編輯管線。 | x |
| 步驟讀取 | 請參閱步驟品質度量結果。 | x | x | x | x | x |

## 資源隔離 {#resource-isolation}

使用的 [!UICONTROL Cloud Manager] 客戶需要其IMS認證進行驗證，因為所有系結到的 [!UICONTROL Cloud Manager] 權限都會設定並系結至其IMS組織。在登入程序中，布建團隊可確保資源隔離 [!UICONTROL Cloud Manager]。

## 資料安全性 {#data-security}

程式碼會 [!UICONTROL Cloud Manager] 在傳輸時加密。Bind Manager Build Build也會在傳輸時加密，並在儲存時加密。

每位客戶都會取得其專屬 **的** Git存放庫，其程式碼會安全，而不會與任何其他 **組織共用**。

## 資料隱私權 {#data-privacy}

[!UICONTROL Cloud Manager] 遵守Adobe所定義的隱私權原則。開發人員可透過HTTPS安全地將程式碼推送至 **Git存放庫** 。

[！DNL使用者介面(UI [!UICONTROL Cloud Manager])建立在符合Adobe定義的通用控制架構之上的服務之上。[！DNL使用者介面(UI)使用 [!UICONTROL Cloud Manager]來自多個雲端供應商的安全服務。
