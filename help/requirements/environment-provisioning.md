---
title: 環境設定
description: 瞭解如何在Cloud Manager登機過程中配置您的環境。
exl-id: eade4255-89b5-4c65-a498-1c6d4e8c73ff
source-git-commit: d033b7cf53d4d9faf074f1dc09e2958eb91afe3b
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---


# 環境設定 {#environments-provisioning}

瞭解如何在Cloud Manager登機過程中配置您的環境。

## 設定 {#provisioning}

在登入過程中，您購買AEM的所有雲環境都通過Adobe自動配置，並連結回其程式， [!UICONTROL Cloud Manager]。 這AEM些雲環境包括在每個Adobe托管服務訂閱中，通常由至少一個生產環境、一個分段環境以及可選的一個或多個開發或測試環境組成。

## 歡迎電子郵件 {#welcome-email}

在完成環境預配過程後，指定的客戶管理員將收到一封歡迎電子郵件，並確認他們已被授予訪問Adobe的權限 [!UICONTROL Experience Cloud]。 歡迎電子郵件包含有關如何開始使用的詳細資訊 [!UICONTROL Experience Cloud] 服務， [!UICONTROL AEM Managed Services] 雲環境以及 [!UICONTROL Cloud Manager] 自助服務門戶。 此外，電子郵件還包含重要資訊，如客戶成功工程師(CSE)聯繫資訊、支援資源、論壇、常見問題解答等。 在電子郵件中提供的資源清單中，您還將獲得有關如何訪問的詳細資訊 [!UICONTROL Cloud Manager] 為雲環AEM境提供。

## 後續步驟 {#next-steps}

收到歡迎電子郵件後，您可以登錄到 [!UICONTROL Cloud Manager] 使用Adobe IMS憑據作為系統管理員。 登錄後，您將能夠驗證您的雲生產AEM和非生產環境是否可用且運行成功。

這些AEM雲環境將由 [!UICONTROL Cloud Manager] 在部署代碼時執行CI/CD管道，從 [!UICONTROL Cloud Manager]的git儲存庫，通過暫存環境，直AEM到生產環境。 您還可以直接從AEM雲環境 [!UICONTROL Cloud Manager] 當您準備為Web屬性建立數字型驗時。
