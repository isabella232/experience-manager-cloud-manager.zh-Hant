---
title: 新增使用者和角色
seo-title: 新增使用者和角色
description: 瞭解使用者和角色，以及如何使用Admin Console來建立描述檔
seo-description: 您可以將使用者新增至Admin Console中的Cloud Manager產品設定檔，以指派特定角色成員資格。 請依照本節的說明進一步瞭解。
uuid: fa204c28-83df-48bb-8360-e158f080dee7
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: requirements
discoiquuid: 1b421993-22c3-4de0-ba64-c1080d07ad5e
feature: 使用者角色
translation-type: tm+mt
source-git-commit: c5d32d49782c899d013fcc60b9c4d2b67e9350ae
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 28%

---


# 新增使用者和角色 {#add-users-and-roles}

[!UICONTROL Cloud Manager]中的許多功能需要特定權限才能運作。 例如，僅允許某些用戶為程式設定關鍵績效指標(KPI)。 這些權限在邏輯上分組為角色。

[!UICONTROL Cloud Manager] 目前為控制特定功能可用性的使用者定義四個角色：

* 企業負責人
* 計畫經理
* 部署管理員
* 開發人員

>[!CAUTION]
>
>若要使用[!UICONTROL Cloud Manager]，您必須有Adobe ID和Adobe Managed Services產品內容。

## 角色定義{#role-definitions}

>[!NOTE]
>
>Admin Console中的「開發人員角色」與[!UICONTROL Cloud Manager]中的「開發人員角色」無關。

下表匯總了角色：

| [!UICONTROL Cloud Manager] 角色 | 說明 |
|--- |--- |
| 企業負責人 | 負責定義KPI、批准生產部署及覆寫重要的3層故障。 |
| 計畫經理 | 使用[!UICONTROL Cloud Manager]執行團隊設定、檢閱狀態及檢視KPI。 可以批准重要的3層故障。 |
| 部署管理員 | 管理部署操作。 使用[!UICONTROL Cloud Manager]執行階段／生產部署。 可編輯CI/CD管線。 可以批准重要的3層故障。 可以訪問Git儲存庫。 |
| 開發人員 | 開發並測試自訂的應用程式碼。 主要使用[!UICONTROL Cloud Manager]來檢視狀態。 可以訪問Git儲存庫以進行代碼提交。 |
| 客戶成功工程師 | 通常支援AMS客戶的成功。 與[!UICONTROL Cloud Manager]互動，以執行需要CSE監督的部署。 |
| 內容作者 | 通常不與[!UICONTROL Cloud Manager]互動。 可使用[!UICONTROL Cloud Manager] Program Switcher（已從[!UICONTROL Experience Cloud]導航）訪問AEM。 |

## 使用Admin Console建立配置檔案{#using-admin-console-to-create-a-profile}

從Adobe Admin Console為[!UICONTROL Cloud Manager]管理角色。 將用戶添加到Admin Console中的[!UICONTROL Cloud Manager]產品配置檔案中，可提供特定角色成員資格。

您可以在Adobe Admin console中將使用者新增至 [!UICONTROL Cloud Manager]**Product Profile** ，以指派特定角色會籍。Adobe Admin console是管理整個組織中Adobe權益的集中位置。若要進一步瞭解Adobe Admin Console，請參閱 [Admin Console的檔案](https://helpx.adobe.com/tw/enterprise/using/admin-console.html)。

>[!NOTE]
>
>若要存取管理控制台並設定您的團隊（使用者和角色），請開啟瀏覽器並造訪[https://adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise)。

為了為 [!UICONTROL Cloud Manager]  (客戶組織中的管理員) 使用者提供適當的角色型權限，必須在 ****[!UICONTROL AEM Managed Services] Product Context下建立新的產品設定檔。

要為[!UICONTROL Cloud Manager]用戶提供相應的基於角色的權限，作為管理員，您必須在[!UICONTROL AEM Managed Services]產品上下文下建立四個新的產品配置檔案，這四個產品配置檔案分別對應於四個[!UICONTROL Cloud Manager]角色：

* 企業負責人
* 部署管理員
* 開發人員
* 計畫經理

您可以使用[](https://adminconsole.adobe.com/)Admin Console[!UICONTROL Cloud Manager]為建立或新增使用者／群組至這些產品描述檔，如下圖所示：

1. 登入管理控制台，然後按一下「新增描述檔&#x200B;**」以新增描述檔。**

   ![](assets/admin_console_roles-1.png)

1. 填寫欄位以設定[!UICONTROL Cloud Manager]的新角色。

   輸入 **描述檔名**、 **顯示名稱** ，以建立新的描述檔。此外，您也可以為描述 **檔選取「權限群組** 」。

   按一下&#x200B;**Done**&#x200B;完成配置檔案建立步驟。

   >[!NOTE]
   >
   >建立這些產品設定檔時，「顯 **示名稱** 」必須是 [!UICONTROL Cloud Manager]定義的技術值  (請參閱下表)。The **Profile Name** can be anything, buth foun commuse, it is recommended to use the values in *Recommended Profile Name* column below.若要這麼做，在建立產品描述檔時，請取消勾選「與描述檔名 **稱相同** 」，並指定對應的值為 **「顯示名稱」**。

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

