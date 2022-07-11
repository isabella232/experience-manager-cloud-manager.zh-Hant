---
title: 新增使用者和角色
description: 瞭解如何使用Admin Console添加用戶和角色以及建立配置檔案。
exl-id: 40086cf0-a1c4-4dde-9dbf-84ea5fa53b84
source-git-commit: b0dbb602253939464ff034941ffbad84b7df77df
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 13%

---


# 新增使用者和角色 {#add-users-and-roles}

中的許多功能 [!UICONTROL Cloud Manager] 需要特定權限才能使用。 例如，只允許某些用戶為程式設定關鍵績效指標(KPI)。 這些權限按邏輯分組為角色。

[!UICONTROL Cloud Manager] 當前為控制特定功能可用性的用戶定義四個角色：

* 業務所有者
* 程式管理器
* 部署管理器
* 開發人員

>[!NOTE]
>
>要使用 [!UICONTROL Cloud Manager]，必須具有Adobe ID和Adobe托管服務產品上下文。

## 角色定義 {#role-definitions}

此表匯總了這些角色。

| [!UICONTROL Cloud Manager] 角色 | 說明 |
|--- |--- |
| 業務所有者 | 此用戶負責定義KPI、審批生產部署，並在必要時覆蓋重要的3層故障。 |
| 程式管理器 | 此用戶使用 [!UICONTROL Cloud Manager] 要執行團隊設定、複查狀態、查看KPI，並可以在必要時批准重要的3層故障。 |
| 部署管理器 | 此用戶管理部署操作並使用 [!UICONTROL Cloud Manager] 要執行暫存/生產部署，請編輯CI/CD管道，在必要時批准重要的3層故障，並可以訪問git儲存庫。 |
| 開發人員 | 此用戶開發和test自定義應用程式碼，主要使用 [!UICONTROL Cloud Manager] 查看部署狀態，並可以訪問git儲存庫以執行代碼提交。 |
| 客戶成功工程師 | 此用戶通常支援AMS客戶的客戶成功，並與 [!UICONTROL Cloud Manager] 執行需要CSE監督的部署。 |
| 內容作者 | 此用戶通常不與 [!UICONTROL Cloud Manager] 但可以利用 [!UICONTROL Cloud Manager] 程式切換器AEM。 |

>[!NOTE]
>
>Admin Console中的開發人員角色與中的開發人員角色無關 [!UICONTROL Cloud Manager]。

## 使用Admin Console建立配置檔案 {#using-admin-console-to-create-a-profile}

[!UICONTROL Cloud Manager] 角色是從Admin Console中管理的。 通過將用戶添加到 [!UICONTROL Cloud Manager] 產品配置檔案。

Admin Console是管理整個組織中的Adobe權利的中心位置。 要瞭解有關Adobe Admin Console的更多資訊，請參閱 [Admin Console。](https://helpx.adobe.com/tw/enterprise/using/admin-console.html)

>[!NOTE]
>
>要訪問管理控制台並設定您的團隊（用戶和角色），請訪問 [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com)。

為了提供相應的基於角色的權限 [!UICONTROL Cloud Manager] 用戶，客戶組織中的管理員必須在 [!UICONTROL AEM Managed Services] 對應於四個產品中每一個的產品上下文 [!UICONTROL Cloud Manager] 角色：

* 業務所有者
* 部署管理器
* 開發人員
* 程式管理器

您可以使用Admin Console建立用戶/組或將用戶/組添加到這些產品配置檔案中。

1. 登錄到Admin Console並按一下 **新建配置檔案** 的子菜單。

   ![新建配置檔案](/help/assets/admin_console_roles-1.png)

1. 提供資訊以設定新角色 [!UICONTROL Cloud Manager]。

   * **設定檔名稱**
   * **顯示名稱**
   * **權限組**

1. 按一下 **完成** 完成建立配置檔案步驟。

建立產品配置檔案時， **顯示名稱** 必須是由定義的技術值 [!UICONTROL Cloud Manager] （見下表）。 The **Profile Name** can be anything, buth foun commuse, it is recommended to use the values in **Recommended Profile Name** column. 若要這麼做，在建立產品描述檔時，請取消勾選「與描述檔名 **稱相同** 」，並指定對應的值為 **「顯示名稱」**。

| **角色** | **顯示名稱（必需）** | **推薦的配置檔案名稱** |
|---|---|---|
| 業務所有者 | `CM_BUSINESS_OWNER_ROLE_PROFILE` | [!UICONTROL Cloud Manager]  — 業務所有者角色 |
| 部署管理器 | `CM_DEPLOYMENT_MANAGER_ROLE_PROFILE` | [!UICONTROL Cloud Manager]  — 部署管理器角色 |
| 開發人員 | `CM_DEVELOPER_ROLE_PROFILE` | [!UICONTROL Cloud Manager]  — 開發人員角色 |
| 程式管理器 | `CM_PROGRAM_MANAGER_ROLE_PROFILE` | [!UICONTROL Cloud Manager]  — 計畫經理角色 |

![建立新配置檔案](/help/assets/screen_shot_2018-05-04at171819.png)

建立產品配置檔案後，您可以將用戶（或組）添加到這些產品配置檔案中。

![編輯用戶](/help/assets/image2018-4-9_15-19-26.png)

![用戶組](/help/assets/image2018-4-9_15-16-47.png)
