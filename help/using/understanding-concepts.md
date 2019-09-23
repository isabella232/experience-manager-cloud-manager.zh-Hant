---
title: 使用Cloud manager前先瞭解概念
seo-title: 使用Cloud manager前先瞭解概念
description: 'null'
seo-description: 'null'
page-status-flag: 從未激活
uuid: 55cc551a-e812-4102-96c8-13d2cdd79c84
contentOwner: jsyal
discoiquuid: c3fd3f4e-0b57-4377-b923-a440c74773d8
preview: 'true'
translation-type: tm+mt
source-git-commit: f135526c6a47f1502395e6d53f9e286c0f935da5

---


# 使用Cloud manager前先瞭解概念{#understanding-concepts-before-using-cloud-manager}

本節提供在使用Cloud manager之前最好瞭解的概念和術語，並涵蓋以下主題：

* **部署環境**
* **原始碼儲存庫**
* **安全性與隱私權**
* **管線概述**
* **說明資源**

## 部署環境 {#deployment-environment}

您可能是Adobe Experience Manager(AEM)6.4的新手，或需要升級至AEM 6.4版本。

如果您是AEM 6.4的新手，則您已擁有Cloud manager的存取權。

如果您是現有客戶，則需要升級至AEM 6.4才能存取Cloud Manager。 一旦您收到客戶成功工程師(CSE)的URL和認證，就可以開始使用Cloud Manager。

<!-- 

Comment Type: annotation
Last Modified By: ptager
Last Modified Date: 2018-05-02T17:19:24.147-0400

Section is redundant with the section in the Overview topic

 -->

## 原始碼儲存庫 {#source-code-repository}

**多個Git伺服器**:在某些情況下，客戶會擁有現有的git儲存庫，並想繼續使用它。

在這些情況下，您可以使用git對多個遠程儲存庫的支援。 日常開發將繼續發生在您的git儲存庫中。 當需要部署時，您只需將最新程式碼推送至Cloud Manager git儲存庫。

<!-- 

Comment Type: annotation
Last Modified By: ptager
Last Modified Date: 2018-05-02T17:20:46.002-0400

Looks like we lost some content, compared to the previous version

 -->

## 安全性與隱私權 {#security-and-privacy}

<!-- 

Comment Type: annotation
Last Modified By: jsyal
Last Modified Date: 2018-04-21T02:38:21.417-0400

Query for Brad B.

 -->

## 管線概述 {#pipeline-overview}

Cloud manager將支援每個計畫（上述定義）的單一管道，以處理部署到舞台和生產環境。 ****

用於舞台和生產部署的Git分支是主要的。

>[!NOTE]
>
>將master當做舞台和生產的Git分支使用是最佳做法，但您可以在設定管道時使用任何分支。

單一管線流程說明如下：

![](assets/screen_shot_2018-04-30at30318pm.png)

### 瞭解流程 {#understanding-the-flow}

您可以從Cloud Manager UI的圖 [!UICONTROL Pipeline Settings] 格設定您的管道。

如需詳 [細資訊，請參閱](hhttps://helpx.adobe.com/experience-manager/cloud-manager/using/using-cloud-manager.html) 「使用Cloud Manager」。

部署管理器負責設定管道，即：

* 分配應用程式分支
* 分配部署環境
* 定義測試選項

執行此操作時，首先從其git儲存庫中選擇一個分支。 接下來，定義將啟動管線的觸發器。

接著，您可以定義控制生產部署的參數。

最後，您將能夠配置效能測試參數。

>[!NOTE]
>
>如要瞭解如何設定管道的行為和偏好設定，請參 **閱使用Cloud manager中的「設** 定管道」一節 [](using-cloud-manager.md)。

### 說明資源 {#help-resources}

請聯絡Adobe管理服務客戶成功工程師以取得支援。

### 後續步驟 {#the-next-steps}

現在您對Cloud manager概念有了更深入的瞭解。

要設定項目、環境和團隊（用戶和角色），請參 [閱設定Cloud manager的常規配置](setting-configurations-for-cloud-manager.md)。
