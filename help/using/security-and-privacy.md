---
title: 安全性與隱私權
seo-title: Cloud Manager的安全AEM性與隱私權
description: 請依照本頁來瞭解資產（程式碼／物件）的安全性和隱私權。
seo-description: 請依照本頁，瞭解使用Cloud Manager的資產（程式碼／物件）的安全性和隱AEM私權。
uuid: 68bc2330-a62c-4c2c-925c-daa6788b143a
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: introduction
discoiquuid: 67a54bae-99a9-4405-91e3-9a0a8b3ccc98
feature: 快速入門
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 3%

---


# 安全性與隱私權 {#security-and-privacy}

[!UICONTROL Cloud Manager] 具有具有適當權限的預先配置角色。本節重點說明使用Cloud Manager的資產（程式碼／物件）的安全性AEM和隱私權。 此外，[!UICONTROL Cloud Manager]還具有預先設定的具有適當權限的角色。

要瞭解可以在Admin Console和用戶角色權限中分配的角色，請參閱[基於角色的權限](/help/using/role-based-permissions.md)。


## 資源隔離{#resource-isolation}

使用[!UICONTROL Cloud Manager]的客戶將需要其IMS憑證來驗證，因為系結至[!UICONTROL Cloud Manager]的所有權限都會設定並系結至其IMS組織。 在上線過程中，設定團隊確保在[!UICONTROL Cloud Manager]中強制執行資源隔離。

## 資料安全{#data-security}

[!UICONTROL Cloud Manager]中的代碼在傳輸中被加密。 Cloud Manager構建的二進位檔案在傳輸中也會加密，並在儲存時加密。

每個客戶都有自己的&#x200B;**Git儲存庫**，其代碼是安全的，不與任何其他&#x200B;**組織**&#x200B;共用。

## 資料隱私{#data-privacy}

[!UICONTROL Cloud Manager] 遵守Adobe所定義的隱私權原則。開發人員可透過HTTPS將程式碼安全地推送至&#x200B;**Git Repository**。

[!UICONTROL Cloud Manager]的使用者介面(UI)建立在符合由Adobe定義之通用控制架構的服務之上。 [!UICONTROL Cloud Manager]的使用者介面使用來自數個雲端提供者的安全服務。
