---
title: 安全性與隱私權
seo-title: AEM Cloud Manager的安全性與隱私權
description: 請依照本頁來瞭解資產（程式碼／物件）的安全性和隱私權。
seo-description: 請依照本頁來瞭解使用AEM Cloud Manager的資產（程式碼／物件）的安全性和隱私權。
uuid: 68bc2330-a62c-4c2c-925c-daa6788b143a
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: introduction
discoiquuid: 67a54bae-99a9-4405-91e3-9a0a8b3ccc98
translation-type: tm+mt
source-git-commit: e2187565e7f06d64841eb2af9b4b1a56feb5ebe4
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 2%

---


# 安全性與隱私權 {#security-and-privacy}

[!UICONTROL Cloud Manager] 具有具有適當權限的預先配置角色。 本節重點說明使用AEM Cloud Manager的資產（程式碼／物件）的安全性和隱私權。 此外， [!UICONTROL Cloud Manager] 已預先設定具有適當權限的角色。

若要瞭解您可在「管理控制台」中指派的角色和使用者角色權限，請參閱「基於角 [色的權限」](/help/using/role-based-permissions.md)。


## 資源隔離 {#resource-isolation}

使用其 [!UICONTROL Cloud Manager] IMS認證的客戶將需要驗證，因為系結至其IMS [!UICONTROL Cloud Manager] 組織的所有權限都會加以設定並系結。 在上線過程中，設定團隊確保在中強制執行資源隔離 [!UICONTROL Cloud Manager]。

## 資料安全性 {#data-security}

在傳輸中 [!UICONTROL Cloud Manager] 的代碼是加密的。 Cloud Manager構建的二進位檔案在傳輸中也會加密，並在儲存時加密。

每個客戶都有自己的 **Git儲存庫** ，其代碼是安全的，不會與任何其他組 **織共用**。

## 資料隱私 {#data-privacy}

[!UICONTROL Cloud Manager] 遵守Adobe所定義的隱私權原則。 開發人員透過HTTPS將程式碼安全地推 **送至Git Repository** 。

適用的使用者介面(UI) [!UICONTROL Cloud Manager] 建立在符合Adobe所定義之通用控制架構的服務之上。 使用者介面， [!UICONTROL Cloud Manager] 以使用來自數家雲端供應商的安全服務。
