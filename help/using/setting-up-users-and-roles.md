---
title: 添加用戶和角色
seo-title: 添加用戶和角色
description: 'null'
seo-description: 您可以將使用者新增至管理控制台中的Cloud manager產品設定檔，以指派特定角色成員資格。 請依照本節的說明進一步瞭解。
uuid: fa204c28-83df-48bb-8360-e158f080dee7
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: 需求
discoiquuid: 1b421993-22c3-4de0-ba64-c1080d07ad5e
translation-type: tm+mt
source-git-commit: 73203dca7b20570103af429cf933610941b787be

---


# 添加用戶和角色{#add-users-and-roles}

中的許多功 [!UICONTROL Cloud Manager] 能需要特定的操作權限。 例如，僅允許某些用戶為程式設定關鍵績效指標(KPI)。 這些權限在邏輯上分組為角色。

[!UICONTROL Cloud Manager] 目前為控制特定功能可用性的使用者定義四個角色：

* 企業負責人
* 計畫經理
* 部署管理員
* 開發人員

>[!CAUTION]
>
>若要使 [!UICONTROL Cloud Manager]用，您必須擁有Adobe ID和Adobe Managed services產品內容。

## 角色定義 {#role-definitions}

>[!NOTE]
>
>「管理控制台」中的「開發人員角色」與中的「開發人員角色」無關 [!UICONTROL Cloud Manager]。

下表匯總了角色：

| [!UICONTROL Cloud Manager] 角色 | 說明 |
|--- |--- |
| 企業負責人 | 負責定義KPI、批准生產部署及覆寫重要的3層故障。 |
| 計畫經理 | 用於 [!UICONTROL Cloud Manager] 執行團隊設定、複查狀態和查看KPI。 可以批准重要的3層故障。 |
| 部署管理員 | 管理部署操作。 用於 [!UICONTROL Cloud Manager] 執行階段／生產部署。 可編輯CI/CD管線。 可以批准重要的3層故障。 可以訪問Git儲存庫。 請連絡您的CSE/AMS代表以索取。 |
| 開發人員 | 開發並測試自訂的應用程式碼。 主要用 [!UICONTROL Cloud Manager] 於查看狀態。 應取得程式碼提交的Git儲存庫存取權。 在添加具有此角色的用戶以授予對Git儲存庫的訪問權時，請聯繫您的CSE/AMS代表。 |
| 客戶成功工程師 | 通常支援AMS客戶的成功。 為執行需 [!UICONTROL Cloud Manager] 要CSE監督的部署而與之互動。 |
| 內容作者 | 通常不與互動 [!UICONTROL Cloud Manager]。 可能會使 [!UICONTROL Cloud Manager] 用Program Switcher(已瀏覽過 [!UICONTROL Experience Cloud])來存取AEM。 |

>[!NOTE]
>
>對 [!UICONTROL Cloud Manager] Git儲存庫的訪問由CSE管理。 請連絡他們以新增和移除使用者。
>
>如果新添加的用戶需要訪問Git儲存庫，則您需要聯繫您的CSE/AMS代表以獲得訪問權限。 這些角色不提供對Git儲存庫的自動訪問。 最多只能有3個具有Git儲存庫訪問權限的用戶。

## 使用Admin console建立設定檔 {#using-admin-console-to-create-a-profile}

角色是從Adobe Admin [!UICONTROL Cloud Manager] Console管理的。 將使用者新增至「管理控制台」中的「產品設定檔」，即可 [!UICONTROL Cloud Manager] 提供特定角色成員資格。

您可以在Adobe Admin console中將使用者新增至產品設定檔，以指派特定的角色會籍。Adobe Admin Console是管理整個組織中Adobe權益的集中位置。 [!UICONTROL Cloud Manager]**** 若要進一步瞭解Adobe Admin Console，請參閱 [Admin Console的檔案](https://helpx.adobe.com/enterprise/using/admin-console.html)。

>[!NOTE]
>
>若要存取管理控制台並設定您的團隊（使用者和角色），請開啟瀏覽器並造訪 [https://adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise)。

為了向用戶提供適當的基於角色的權限， [!UICONTROL Cloud Manager] 客戶組織中的管理員必須在「產品上下文」( ****[!UICONTROL AEM Managed Services] Product Context)下建立新的「產品配置檔案」(Product Profiles)。

要向用戶提供適當的基於角色的權限， [!UICONTROL Cloud Manager] 作為管理員，您必須在「產品上下文」( [!UICONTROL AEM Managed Services] Product Context)下建立四個新的「產品配置檔案」(Product Profiles)，分別對應於以下四個 [!UICONTROL Cloud Manager] 角色：

* 企業負責人
* 部署管理員
* 開發人員
* 計畫經理

您可以使用 [Admin Console](https://adminconsole.adobe.com/) [!UICONTROL Cloud Manager]for建立或新增使用者／群組至這些產品設定檔，如下圖所示：

1. 登入管理控制台，然後按一下「 **新增描述檔** 」以新增描述檔。

   ![](assets/admin_console_roles-1.png)

1. 填寫欄位以設定新角色 [!UICONTROL Cloud Manager]。

   輸入 **描述檔名**、 **顯示名稱** ，以建立新的描述檔。 此外，您也可以為描述 **檔選取「權限群組** 」。

   按一下「 **完成** 」(Done)以完成配置檔案建立步驟。

   >[!NOTE]
   >
   >建立這些產品描述檔時， **「顯示名稱** 」必須是由定義的 [!UICONTROL Cloud Manager] 技術值（請參閱下表）。 The **Profile Name** can be anything, buth foun commuse, it is recommended to use the values in *Recommended Profile Name* column below. 若要這麼做，在建立產品描述檔時，請取消勾選「與描述檔名 **稱相同** 」，並指定對應的值為 **「顯示名稱」**。

   | **角色** | **顯示名稱（必要）** | **建議的描述檔名稱** |
   |---|---|---|
   | 企業負責人 | CM_BUSINESS_OWNER_ROLE_PROFILE | [!UICONTROL Cloud Manager] -企業所有者角色 |
   | 部署管理員 | CM_DEPLOYMENT_MANAGER_ROLE_PROFILE | [!UICONTROL Cloud Manager] -部署管理員角色 |
   | 開發人員 | CM_DEVELOPER_ROLE_PROFILE | [!UICONTROL Cloud Manager] -開發人員角色 |
   | 計畫經理 | CM_PROGRAM_MANAGER_ROLE_PROFILE | [!UICONTROL Cloud Manager] -計畫經理角色 |

   ![](assets/screen_shot_2018-05-04at171819.png)

1. 在您建立產品設定檔後，就可以新增使用者（或群組）至這些產品設定檔。

   ![](assets/image2018-4-9_15-19-26.png)

   ![](assets/image2018-4-9_15-16-47.png)

