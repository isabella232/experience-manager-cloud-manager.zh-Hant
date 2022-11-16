---
title: 環境佈建
description: 了解如何將您的環境佈建為 Cloud Manager 上線流程的一部分。
exl-id: eade4255-89b5-4c65-a498-1c6d4e8c73ff
source-git-commit: d033b7cf53d4d9faf074f1dc09e2958eb91afe3b
workflow-type: ht
source-wordcount: '314'
ht-degree: 100%

---


# 環境佈建 {#environments-provisioning}

了解如何將您的環境佈建為 Cloud Manager 上線流程的一部分。

## 佈建 {#provisioning}

在上線流程中，您已經購買的所有 AEM 雲端環境都會由 Adobe 自動佈建，並連結回這些環境在 [!UICONTROL Cloud Manager] 中的方案。每個 Adob&#x200B;&#x200B;e Managed Services 訂閱中都會包含這些 AEM 雲端環境，並通常會由至少一個生產環境、一個中繼環境以及一個或多個開發或測試環境 (可選) 組成。

## 歡迎電子郵件 {#welcome-email}

完成環境佈建流程後，指定的客戶管理員即會收到一封歡迎電子郵件，確認已授予他們對 Adobe [!UICONTROL Experience Cloud] 的存取權。此歡迎電子郵件會包含有關如何開始使用 [!UICONTROL Experience Cloud] 服務、[!UICONTROL AEM Managed Services] 雲端環境以及 [!UICONTROL Cloud Manager] 自助服務入口網站的詳細資訊。此外，該電子郵件還會包含一些重要資訊，例如客戶成功工程師 (CSE) 聯絡資訊、何處可取得支援資源、論壇、常見問題集等。在電子郵件中提供的資源清單中，您還將取得有關如何為您的 AEM 雲端環境存取 [!UICONTROL Cloud Manager] 的詳細資訊。

## 後續步驟 {#next-steps}

在收到歡迎電子郵件後，您就能使用您的 Adobe IMS 憑證，以系統管理員的身分登入 [!UICONTROL Cloud Manager]。登入後，您將能夠驗證您的 AEM 雲端生產和非生產環境是否可供使用並可成功運作。

部署程式碼時，[!UICONTROL Cloud Manager] 將使用這些 AEM 雲端環境來執行 CI/CD 管道，從 [!UICONTROL Cloud Manager] 的 Git 存放庫開始，通過中繼環境，一直到您的 AEM 生產環境。當您準備好要開始建立 Web 屬性的數位體驗時，您還將能夠直接從 [!UICONTROL Cloud Manager] 存取您的 AEM 雲端環境。
