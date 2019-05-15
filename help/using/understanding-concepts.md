---
title: 使用雲端管理員瞭解概念
seo-title: 使用雲端管理員瞭解概念
description: 'null'
seo-description: 'null'
page-status-flag: 從未啓動
uuid: 55cc551a-e812-4102-96c8-13d2 cdd79 c84
contentOwner: jsyal
discoiquuid: c3fd3f4e-0b57-4377-b923-a440 c74773 d
preview: 'true'
translation-type: tm+mt
source-git-commit: 1dfb065c09569f811e5a006d3d74825d3bd7cc8d

---


# 使用雲端管理員瞭解概念{#understanding-concepts-before-using-cloud-manager}

本節提供在Cloud Manager中操作前很容易知道的概念和術語，並涵蓋下列主題：

* **部署環境**
* **原始碼存放庫**
* **安全性與隱私權**
* **管道概述**
* **說明資源**

## 部署環境 {#deployment-environment}

您可能是Adobe Experience Manager(AEM)6.4的新手，或需要升級至AEM6.4版本。

如果您是AEM6.4的新功能，則您已擁有Cloud Manager的存取權。

如果您是現有客戶，則需要升級至AEM6.4才能存取Cloud Manager。當您收到客戶成功工程師(CSE)的URL和認證後，就可以開始使用Cloud Manager。

<!-- 

Comment Type: annotation
Last Modified By: ptager
Last Modified Date: 2018-05-02T17:19:24.147-0400

Section is redundant with the section in the Overview topic

 -->

## 原始碼存放庫 {#source-code-repository}

**多個Git伺服器**：在某些情況下，客戶將擁有現有的git存放庫，並且想要繼續使用它。

在這種情況下，您可以使用git對多個遠端儲存庫的支援。每日開發將繼續發生在您的Git存放庫中。當需要部署時，您只需將最新代碼推送至Cloud Manager Git存放庫即可。

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

## 管道概述 {#pipeline-overview}

Cloud Manager將支援每個方案(定義為上述定義)，以處理部署至階段和生產。****

用於舞台和生產部署的git分支是主版。

>[!NOTE]
>
>將主版用作舞台和生產的分支是最佳做法，但您可以在設定管線時使用任何分支。

單一管線程序如下所示：

![](assets/screen_shot_2018-04-30at30318pm.png)

### 瞭解流程 {#understanding-the-flow}

您可以從雲端管理員UI中，從 [!UICONTROL Pipeline Settings] 方塊設定渠道。

如需詳細資訊，請參閱 [使用Cloud](hhttps://helpx.adobe.com/experience-manager/cloud-manager/using/using-cloud-manager.html) Manager。

部署管理員負責設定管道，即：

* 指派應用程式分支
* 指派部署環境
* 定義測試選項

此時，您會先從其git存放庫中選取分支。接著，定義將啓動管線的觸發器。

接著，您可以定義控制生產部署的參數。

最後，您將能夠設定效能測試參數。

>[!NOTE]
>
>如需瞭解渠道的行為和偏好設定，請參閱 **使用Cloud Manager中的「設定管道」**[區段](using-cloud-manager.md)。

### 說明資源 {#help-resources}

聯絡Adobe Managed Services客戶成功工程師以取得支援。

### 後續步驟 {#the-next-steps}

現在您更能瞭解Cloud Manager概念。

若要設定您的專案、環境以及團隊(使用者和角色)，請參閱 [設定Cloud Manager的一般設定](setting-configurations-for-cloud-manager.md)。
