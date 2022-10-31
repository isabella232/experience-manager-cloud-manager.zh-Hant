---
title: 新增使用者和角色
description: 了解如何使用 Admin Console 新增使用者和角色，並建立設定檔。
exl-id: 40086cf0-a1c4-4dde-9dbf-84ea5fa53b84
source-git-commit: dd96d773ea3e6b9c45886fe41b28d3dd70cb8a61
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 22%

---


# 新增使用者和角色 {#add-users-and-roles}

中的許多功能 [!UICONTROL Cloud Manager] 需要特定權限才能使用。 例如，僅允許某些使用者為方案設定關鍵績效指標 (KPI)。這些權限在邏輯上會按角色分組。

[!UICONTROL Cloud Manager] 目前會為使用者定義四個角色，以控管特定功能的可用性：

* 企業所有者
* 方案管理員
* 部署管理員
* 開發人員

>[!NOTE]
>
>使用 [!UICONTROL Cloud Manager]，您必須有Adobe ID和Adobe Managed Services產品內容。

## 角色定義 {#role-definitions}

本表會概述這些角色。

| [!UICONTROL Cloud Manager] 角色 | 說明 |
|--- |--- |
| 企業所有者 | 這類使用者會負責定義 KPI、核准生產部署並在必要時覆寫重要的 3 層級失敗。 |
| 方案管理員 | 此使用者使用 [!UICONTROL Cloud Manager] 若要執行團隊設定、檢閱狀態、檢視KPI，並可視需要核准重要的3層故障。 |
| 部署管理員 | 此用戶管理部署操作並使用 [!UICONTROL Cloud Manager] 若要執行測試/生產部署，請編輯CI/CD管道、視需要核准重要的3層失敗，並可存取git存放庫。 |
| 開發人員 | 此用戶開發和測試自定義應用程式代碼，主要使用 [!UICONTROL Cloud Manager] 若要檢視部署狀態，並可存取git存放庫以進行程式碼提交。 |
| 客戶成功工程師 | 此使用者通常可支援AMS客戶的成功案例，並與 [!UICONTROL Cloud Manager] 執行需要CSE監督的部署。 |
| 內容作者 | 此使用者通常不會與 [!UICONTROL Cloud Manager] 但可以使用 [!UICONTROL Cloud Manager] 程式切換器存取AEM。 |

>[!NOTE]
>
>Admin Console中的開發人員角色與 [!UICONTROL Cloud Manager].

## 使用 Admin Console 建立設定檔 {#using-admin-console-to-create-a-profile}

[!UICONTROL Cloud Manager] 角色是從Admin Console中管理。 通過將用戶添加到 [!UICONTROL Cloud Manager] 產品設定檔。

Admin Console 是在整個組織中管理 Adob&#x200B;&#x200B;e 權益的中心位置。若要了解有關 Adobe Admin Console 的詳細資訊，請參閱 [Admin Console 的文件。](https://helpx.adobe.com/tw/enterprise/using/admin-console.html)

若要提供適當的角色型權限給 [!UICONTROL Cloud Manager] 使用者、客戶組織中的管理員必須在 [!UICONTROL AEM Managed Services] 對應於四個 [!UICONTROL Cloud Manager] 角色：

* 企業所有者
* 部署管理員
* 開發人員
* 方案管理員

您可以使用 Admin Console 建立或新增使用者/群組到這些產品設定檔。

1. 登入Admin Console: [`https://adminconsole.adobe.com`.](https://adminconsole.adobe.com)

1. 按一下 **概述** 頁簽上，按一下要修改的產品 **產品和服務** 卡片。 若未列於此處，請使用 **產品** 索引標籤，找出產品並按一下。

   ![「管理控制台概觀」標籤](/help/assets/admin-console-overview.png)

1. 在 **產品** 標籤，按一下您要將使用者/群組新增至產品設定檔的環境。

   ![Admin Console產品索引標籤](/help/assets/admin-console-product.png)

1. 在 **產品設定檔** ，按一下 **新設定檔** 來新增新設定檔。

   ![新設定檔](/help/assets/admin-console-product-profiles.png)

1. 提供資訊以設定 [!UICONTROL Cloud Manager].

   * **設定檔名稱** - **設定檔名稱** 可為任何值，但為避免混淆，建議在 **建議的設定檔名稱** 欄。
   * **顯示名稱** - **顯示名稱** 必須是 [!UICONTROL Cloud Manager] （請參閱下表）。
   * **權限群組**  — 您可以為設定檔選擇權限群組（不一定可用）。

   ![建立新設定檔](/help/assets/screen_shot_2018-05-04at171819.png)

   | 角色 | 顯示名稱 (必填) | 建議的設定檔名稱 |
   |---|---|---|
   | 企業所有者 | `CM_BUSINESS_OWNER_ROLE_PROFILE` | [!UICONTROL Cloud Manager]  — 業務所有者角色 |
   | 部署管理員 | `CM_DEPLOYMENT_MANAGER_ROLE_PROFILE` | [!UICONTROL Cloud Manager]  — 部署管理員角色 |
   | 開發人員 | `CM_DEVELOPER_ROLE_PROFILE` | [!UICONTROL Cloud Manager]  — 開發人員角色 |
   | 方案管理員 | `CM_PROGRAM_MANAGER_ROLE_PROFILE` | [!UICONTROL Cloud Manager]  — 計畫經理角色 |


1. 按一下 **完成** 以儲存新設定檔。

## 將設定檔指派給使用者或使用者群組 {#assign-profiles}

建立產品設定檔後，您就可以指派使用者或使用者群組給他們。

1. 登入Admin Console: [`https://adminconsole.adobe.com`.](https://adminconsole.adobe.com)

1. 在Admin Console中，選取 **使用者** 標籤。

   ![使用者索引標籤](/help/assets/admin-console-users.png)

1. 按一下 **使用者** 在左側導覽面板中，然後按一下使用者加以修改。

1. 按一下 **產品** 區段，然後選取 **編輯**.

   ![編輯使用者](/help/assets/admin-console-edit-user.png)

1. 在 **編輯產品和使用者群組** 對話框，按一下加號按鈕並選擇要分配給用戶的配置檔案。

   * 如果已將使用者指派給角色，則加號按鈕將是編輯按鈕（鉛筆），但運作方式相同。

   ![編輯產品和使用者群組](/help/assets/admin-console-edit-products-and-user-groups.png)

1. 按一下 **儲存** 將設定檔儲存給使用者。

重複相同步驟，將設定檔指派給使用者群組，但選取 **使用者群組** 從 **使用者** 標籤。 按一下使用者群組，然後選取 **指派的產品設定檔** 按一下 **指派產品設定檔** 來指派設定檔。

![將設定檔指派給群組](/help/assets/admin-console-edit-user-groups.png)
