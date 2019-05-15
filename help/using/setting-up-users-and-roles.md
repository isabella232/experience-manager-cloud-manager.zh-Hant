---
title: 新增使用者和角色
seo-title: 新增使用者和角色
description: 'null'
seo-description: 您可以在管理控制台中新增使用者至Cloud Manager產品描述檔，以指定特定角色會籍。請遵循本節以瞭解更多資訊。
uuid: fa204c28-83df-48bb-8360-e158 f080 dee7
contentOwner: jsyal
products: SG_ PERIENCENCENAGER/CLUDManager
topic-tags: 需求
discoiquuid: 1b421993-22c3-4de0-ba64-c1080 d07 e5 e
translation-type: tm+mt
source-git-commit: 1dfb065c09569f811e5a006d3d74825d3bd7cc8d

---


# 新增使用者和角色{#add-users-and-roles}

許多功能 [!UICONTROL Cloud Manager] 需要特定權限運作。例如，只允許特定使用者設定計劃的關鍵績效指標(KPI)。這些權限會以邏輯方式分組為角色。

[!UICONTROL Cloud Manager] 目前為規範特定功能可用性的使用者定義個角色：

* 企業負責人
* 方案經理
* 部署管理員
* 開發人員

>[!CAUTION]
>
>若要使用 [!UICONTROL Cloud Manager]，您必須擁有Adobe ID和Adobe Managed Services產品上下文。

## 角色定義 {#role-definitions}

>[!NOTE]
>
>「管理控制台」中的「開發人員」角色與「開發人員」角色無關 [!UICONTROL Cloud Manager]。

下表總結角色：

| [!UICONTROL Cloud Manager] 角色 | 說明 |
|--- |--- |
| 企業負責人 | 負責定義KPI、核准生產部署並覆寫重要的層失敗。 |
| 方案經理 | 用於 [!UICONTROL Cloud Manager] 執行團隊設定、檢閱狀態及檢視KPI。可以核准重要的層失敗。 |
| 部署管理員 | 管理部署作業。用於 [!UICONTROL Cloud Manager] 執行階段/生產部署。可以編輯CI/CD管線。可以核准重要的層失敗。可以存取Git存放庫。請聯絡您的CSE/AMS代表以索取此資訊。 |
| 開發人員 | 開發並測試自訂應用程式代碼。主要用於 [!UICONTROL Cloud Manager] 檢視狀態。應存取Git存放庫以進行程式碼提交。新增具有此角色的使用者以授與Git存放庫的存取權時，請連絡您的CSE/AMS代表。 |
| 客戶成功工程師 | 一般支援AMS客戶成功案例。與執行 [!UICONTROL Cloud Manager] 需要CSE監督的部署互動。 |
| 內容作者 | 通常不會與您互動 [!UICONTROL Cloud Manager]。可使用 [!UICONTROL Cloud Manager] Program Switcher(導覽自 [!UICONTROL Experience Cloud])存取AEM。 |

>[!NOTE]
>
>存取 [!UICONTROL Cloud Manager] Git存放庫由您的CSE管理。聯絡他們以新增和移除使用者。
>
>如果新加入的使用者需要存取Git存放庫，您必須聯絡CSE/AMS代表才能取得存取權。這些角色無法自動存取Git存放庫。您最多只能有位擁有Git儲存庫存取權的使用者。

## 使用管理控制台建立描述檔 {#using-admin-console-to-create-a-profile}

角色是由 [!UICONTROL Cloud Manager] Adobe Admin Console管理。您可以在Admin Console中新增使用者至 [!UICONTROL Cloud Manager] 產品描述檔，以提供特定角色會籍。

您可以在Adobe Admin Console中新增使用者至 [!UICONTROL Cloud Manager]**「產品描述檔** 」，指定特定角色會籍，這個中心位置是管理整個組織內Adobe權益的中央位置。若要進一步瞭解Adobe Admin Console，請參閱 [Admin Console的文件](https://helpx.adobe.com/enterprise/using/admin-console.html)。

>[!NOTE]
>
>若要呼叫管理主控台並設定您的團隊(使用者和角色)，請開啓瀏覽器並瀏覽 [https://adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise)。

若要為 [!UICONTROL Cloud Manager] 使用者( **客戶組織**中的管理員)提供適當的角色權限，必須在 [!UICONTROL AEM Managed Services] 產品內容下建立新的產品描述檔。

若要為 [!UICONTROL Cloud Manager] 使用者提供適當的角色權限，身為管理員，您必須在對應四 [!UICONTROL AEM Managed Services][!UICONTROL Cloud Manager] 個角色的「產品內容」下建立四個新的「產品描述檔」：

* 企業負責人
* 部署管理員
* 開發人員
* 方案經理

您可以使用 [「管理控制台」](https://adminconsole.adobe.com/) 建立或新增使用者/群組至這些產品描述檔 [!UICONTROL Cloud Manager]，如下圖所示：

1. 登入管理控制台，然後按一下 **「新增描述檔** 」以新增描述檔。

   ![](assets/admin_console_roles-1.png)

1. 填寫欄位以設定新角色 [!UICONTROL Cloud Manager]。

   輸入 **描述檔名稱**， **顯示名稱** 以建立新的描述檔。此外，您也可以選取描述檔 **的權限群組** 。

   按一下 **完成** ，完成描述檔建立步驟。

   >[!NOTE]
   >
   >建立這些產品設定檔時， **「顯示名稱** 」必須是定義的技術值 [!UICONTROL Cloud Manager] (請參閱下表)。**「描述檔名稱** 」可以是任何項目，但為了避免混淆，建議您在下方的 *「建議個人檔案名稱」* 欄中使用值。若要這麼做，請在建立產品描述檔時取消勾選 **與描述檔名稱** 相同的值，並指定對應的值作為 **顯示名稱**。

   | **角色** | **顯示名稱(必要)** | **建議的描述檔名稱** |
   |---|---|---|
   | 企業負責人 | CM_ TRADE_ OMAR_ PORIER_ PROFILE | [!UICONTROL Cloud Manager] - 業務擁有者角色 |
   | 部署管理員 | CM_ TRANDER_ MANAGER_ SERVER_ PROFILE | [!UICONTROL Cloud Manager] - 部署管理員角色 |
   | 開發人員 | CM_ Developer_ SERVER_ PROFILE | [!UICONTROL Cloud Manager] - 開發人員角色 |
   | 方案經理 | CM_ Program_ Manager_ SERVER_ PROFILE | [!UICONTROL Cloud Manager] - 方案經理角色 |

   ![](assets/screen_shot_2018-05-04at171819.png)

1. 在建立產品描述檔後，您可以新增使用者(或群組)至這些產品描述檔。

   ![](assets/image2018-4-9_15-19-26.png)

   ![](assets/image2018-4-9_15-16-47.png)

