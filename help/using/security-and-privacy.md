---
title: 安全性與隱私權
seo-title: AEM Cloud Manager的安全性和隱私權
description: 請詳閱本頁面，了解資產（程式碼/成品）的安全性和隱私權。
seo-description: 請詳閱本頁，了解使用AEM Cloud Manager的資產（程式碼/成品）的安全性和隱私權。
uuid: 68bc2330-a62c-4c2c-925c-daa6788b143a
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: introduction
discoiquuid: 67a54bae-99a9-4405-91e3-9a0a8b3ccc98
feature: 快速入門
exl-id: 67df1987-8db7-40bd-9717-1bf194e957f7
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 3%

---

# 安全性與隱私權 {#security-and-privacy}

[!UICONTROL Cloud Manager] 已預先設定具有適當權限的角色。本節重點說明使用AEM Cloud Manager的資產（程式碼/成品）的安全性和隱私權。 此外，[!UICONTROL Cloud Manager]還預先配置了具有適當權限的角色。

若要了解您可以在Admin Console和使用者角色權限中指派的可能角色，請參閱[角色型權限](/help/using/role-based-permissions.md)。


## 資源隔離{#resource-isolation}

使用[!UICONTROL Cloud Manager]的客戶將需要其IMS憑證來驗證，因為系結至[!UICONTROL Cloud Manager]的所有權限都會設定並系結至其IMS組織。 在上線過程中，設定團隊確保在[!UICONTROL Cloud Manager]中強制執行資源隔離。

## 資料安全{#data-security}

[!UICONTROL Cloud Manager]中的代碼在傳輸中被加密。 Cloud Manager組建的二進位檔在傳輸中也會經過加密，且儲存時會加密。

每個客戶都有自己的&#x200B;**Git存放庫**，且其程式碼安全無虞，且不會與任何其他&#x200B;**組織**&#x200B;共用。

## 資料隱私{#data-privacy}

[!UICONTROL Cloud Manager] 遵守由Adobe定義的隱私權原則。開發人員透過HTTPS將程式碼安全地推送至&#x200B;**Git存放庫**。

[!UICONTROL Cloud Manager]的使用者介面(UI)是以符合由Adobe定義之通用控制架構的服務為基礎而建置。 [!UICONTROL Cloud Manager]的用戶介面使用來自多個雲提供商的安全服務。
