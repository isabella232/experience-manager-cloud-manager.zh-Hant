---
title: 安全性與隱私權
description: 瞭解Cloud Manager中代碼和項目資產的安全性和隱私性。
exl-id: 67df1987-8db7-40bd-9717-1bf194e957f7
source-git-commit: d7751757c1d3bda3d60406a1d39cb41c61f5c863
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 3%

---


# 安全性與隱私權 {#security-and-privacy}

瞭解Cloud Manager中代碼和項目資產的安全性和隱私性。

## 角色和權限 {#roles}

[!UICONTROL Cloud Manager] 具有預配置的具有適當權限的角色。

要瞭解可以在Admin Console和用戶角色權限中分配的可能角色，請參閱文檔 [基於角色的權限。](/help/requirements/role-based-permissions.md)

## 資源隔離 {#resource-isolation}

[!UICONTROL Cloud Manager] 客戶需要其IMS憑據來驗證是否與所有權限相關 [!UICONTROL Cloud Manager] 與他們的IMS組織有聯繫。 在載入過程中，資源調配團隊確保在 [!UICONTROL Cloud Manager]。

## 資料安全 {#data-security}

中的代碼 [!UICONTROL Cloud Manager] 在傳輸中被加密。 Cloud Manager生成的二進位檔案也在傳輸中加密，並在儲存時加密。

每個客戶都擁有自己的Git儲存庫，並且代碼是安全的，不會與其他任何組織共用。

## 資料隱私 {#data-privacy}

[!UICONTROL Cloud Manager] 遵守了Adobe定義的隱私原則。 開發人員通過HTTPS將代碼安全地推送到Git儲存庫。

[!UICONTROL Cloud Manager]用戶介面構建在符合Adobe通用控制框架的服務之上。 [!UICONTROL Cloud Manager]用戶介面使用來自多個雲提供商的安全服務。
