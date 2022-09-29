---
title: 新增使用者和角色
description: 了解如何使用 Admin Console 新增使用者和角色，並建立設定檔。
exl-id: 40086cf0-a1c4-4dde-9dbf-84ea5fa53b84
source-git-commit: b0dbb602253939464ff034941ffbad84b7df77df
workflow-type: ht
source-wordcount: '536'
ht-degree: 100%

---


# 新增使用者和角色 {#add-users-and-roles}

[!UICONTROL Cloud Manager] 中的許多功能都需要特定權限才能使用。例如，僅允許某些使用者為方案設定關鍵績效指標 (KPI)。這些權限在邏輯上會按角色分組。

[!UICONTROL Cloud Manager] 目前為管控特定功能可用性的使用者定義了四種角色：

* 企業所有者
* 方案管理員
* 部署管理員
* 開發人員

>[!NOTE]
>
>若要使用 [!UICONTROL Cloud Manager]，您必須擁有 Adobe ID 以及 Adobe Managed Services 產品內容。

## 角色定義 {#role-definitions}

本表會概述這些角色。

| [!UICONTROL Cloud Manager] 角色 | 說明 |
|--- |--- |
| 企業所有者 | 這類使用者會負責定義 KPI、核准生產部署並在必要時覆寫重要的 3 層級失敗。 |
| 方案管理員 | 這類使用者會使用 [!UICONTROL Cloud Manager] 來執行團隊設定、審查狀態、檢視 KPI，並可在必要時核准重要的 3 層級失敗。 |
| 部署管理員 | 這類使用者會管理部署操作，並使用 [!UICONTROL Cloud Manager] 來執行中繼/生產部署、編輯 CI/CD 管道、核准重要的 3 層級失敗 (如有必要)，並可存取 Git 存放庫。 |
| 開發人員 | 這類使用者會開發和測試自訂應用程式，並主要使用 [!UICONTROL Cloud Manager] 來檢視部署狀態，且可存取程式碼認可的 Git 存放庫。 |
| 客戶成功工程師 | 這類使用者通常會為 AMS 客戶支援客戶成功，並為了執行需要 CSE 監督的部署會和 [!UICONTROL Cloud Manager] 互動。 |
| 內容作者 | 這類使用者通常不會和 [!UICONTROL Cloud Manager] 互動，但可能會使用 [!UICONTROL Cloud Manager] 方案切換器來存取 AEM。 |

>[!NOTE]
>
>Admin Console 中的「開發人員」角色和 [!UICONTROL Cloud Manager] 中的「開發人員」角色並不相關。

## 使用 Admin Console 建立設定檔 {#using-admin-console-to-create-a-profile}

[!UICONTROL Cloud Manager] 角色會從 Admin Console 進行管理。 透過將使用者新增到 [!UICONTROL Cloud Manager] 產品設定檔，可提供特定的角色會籍。

Admin Console 是在整個組織中管理 Adob&#x200B;&#x200B;e 權益的中心位置。若要了解有關 Adobe Admin Console 的詳細資訊，請參閱 [Admin Console 的文件。](https://helpx.adobe.com/tw/enterprise/using/admin-console.html)

>[!NOTE]
>
>若要存取 Admin Console 及設定您的團隊 (使用者和角色)，請造訪 [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com)。

為了提供角色型權限給 [!UICONTROL Cloud Manager] 使用者，客戶組織中的管理員必須在 [!UICONTROL AEM Managed Services] 產品內容下建立產品設定檔，需對應至以下四個 [!UICONTROL Cloud Manager] 角色的每一個：

* 企業所有者
* 部署管理員
* 開發人員
* 方案管理員

您可以使用 Admin Console 建立或新增使用者/群組到這些產品設定檔。

1. 登入 Admin Console 並按一下&#x200B;**新設定檔**，即可新增設定檔。

   ![新設定檔](/help/assets/admin_console_roles-1.png)

1. 提供資訊以設定 [!UICONTROL Cloud Manager] 的新角色。

   * **設定檔名稱**
   * **顯示名稱**
   * **權限群組**

1. 按一下&#x200B;**完成**，以完成此設定檔建立步驟。

建立產品設定檔時，**顯示名稱**&#x200B;必須是由 [!UICONTROL Cloud Manager] 定義的技術值 (請參閱下表)。**設定檔名稱**&#x200B;可以為任何內容，但為避免混淆，建議使用&#x200B;**建議的設定檔名稱**&#x200B;欄中的值。若要這麼做，在建立產品設定檔時，請取消勾選&#x200B;**與設定檔名稱相同**，並指定對應的值為&#x200B;**顯示名稱**。

| **角色** | **顯示名稱 (必填)** | **建議的設定檔名稱** |
|---|---|---|
| 企業所有者 | `CM_BUSINESS_OWNER_ROLE_PROFILE` | [!UICONTROL Cloud Manager] - 企業所有者角色 |
| 部署管理員 | `CM_DEPLOYMENT_MANAGER_ROLE_PROFILE` | [!UICONTROL Cloud Manager] - 部署管理員角色 |
| 開發人員 | `CM_DEVELOPER_ROLE_PROFILE` | [!UICONTROL Cloud Manager] - 開發人員角色 |
| 方案管理員 | `CM_PROGRAM_MANAGER_ROLE_PROFILE` | [!UICONTROL Cloud Manager] - 計劃管理員角色 |

![建立新設定檔](/help/assets/screen_shot_2018-05-04at171819.png)

您建立產品設定檔後，即可新增使用者 (或群組) 到這些產品設定檔。

![編輯使用者](/help/assets/image2018-4-9_15-19-26.png)

![使用者群組](/help/assets/image2018-4-9_15-16-47.png)
