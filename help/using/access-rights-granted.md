---
title: 授予的存取權限
seo-title: 在AEM Cloud Manager中授予的存取權
description: 進一步瞭解Adobe ID和Experience Cloud資源。
seo-description: 請依照本頁進一步瞭解Adobe ID和AEM Experience Cloud資源。
uuid: 9aa90a99-f049-422e-9e06-b00b843ed98b
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: requirements
discoiquuid: 072dbc1b-e608-4b1f-b0e8-0e4f88c8ad12
translation-type: tm+mt
source-git-commit: e8484052124c23d4849c59f6c76262a3284ef2ac
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 21%

---


# 授予的存取權限 {#access-rights-granted}

## 用戶身份類型 {#user-identity-types}

在上線程式中，Adobe會在Adobe Identity Management System(IMS)中為您的公司建立 **Organization** identifier，以便管理所有使用者及其權限。 每位使用者必須是本組織的成員，且將獲得任何服務的存取權 [!UICONTROL Experience Cloud] ，必須擁有自己的 **Adobe ID**。

若要開始使用Adobe ID，請造訪 [Manage Adobe Identity Types](https://helpx.adobe.com/enterprise/using/identity.html) ，以取得如何使用其中一種可用身分類型取得Adobe ID的詳細指示。

### 使用者和角色 {#users-and-roles}

在Adobe為您的公司建立組織後，您指定的管理員即會新增為該組織的第一名成員。The administrator will be granted the administrator permissions by default, and assigned the [!UICONTROL AEM Managed Services] **Product**, and one or more [!UICONTROL Cloud Manager] **Product Profiles**. 請造訪 [新增使用者和角色](setting-up-users-and-roles.md) ，以進一步瞭解如何使用管理控制台來設定和管理您的團隊使用者。

授予這些權限後，管理員現在會設定單一登入（使用Adobe ID）來存取服務、登入 [!UICONTROL Experience Cloud] AEM雲端環境並使用 [!UICONTROL Cloud Manager]。
