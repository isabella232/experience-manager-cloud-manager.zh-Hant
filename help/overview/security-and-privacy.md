---
title: 安全性與隱私權
description: 了解 Cloud Manager 中程式碼和成品資產的安全性和隱私權。
exl-id: 67df1987-8db7-40bd-9717-1bf194e957f7
source-git-commit: d7751757c1d3bda3d60406a1d39cb41c61f5c863
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 100%

---


# 安全性與隱私權 {#security-and-privacy}

了解 Cloud Manager 中程式碼和成品資產的安全性和隱私權。

## 角色與權限 {#roles}

[!UICONTROL Cloud Manager] 已預先設定角色，並賦予適當權限。 

若要了解有關您在 Admin Console 中可指派的角色以及使用者角色權限，請參閱文件：[角色型權限。](/help/requirements/role-based-permissions.md)

## 資源隔離 {#resource-isolation}

[!UICONTROL Cloud Manager] 客戶需要他們的 IMS 憑證來進行身分驗證，因為所有繫結至 [!UICONTROL Cloud Manager] 的權限都與其 IMS 組織連結。在上線流程中，佈建團隊會確保在 [!UICONTROL Cloud Manager] 中執行資源隔離。

## 資料安全性 {#data-security}

傳輸中會將 [!UICONTROL Cloud Manager] 中的程式碼加密。傳輸過程中還會將 Cloud Manager 建置的二進位檔加密，並在儲存時進行加密。

每個客戶都會有自己的 Git 存放庫，因此程式碼是安全的，不會和任何其他組織共用。

## 資料隱私 {#data-privacy}

[!UICONTROL Cloud Manager] 會遵守由 Adobe 定義的隱私原則。開發人員會經由 HTTPS 將程式碼安全地推送到 Git 存放庫中。

[!UICONTROL Cloud Manager] 的使用者介面會建置在符合 Adobe 一般控制架構的服務上。[!UICONTROL Cloud Manager] 的使用者介面會使用來自數個雲端提供者的安全服務。
