---
title: 原始碼存放庫
seo-title: Adobe雲端管理員的原始AEM碼儲存庫
description: 請依照本頁瞭解為Cloud Manager中的每個程式布建的git儲存庫。
seo-description: 請依照本頁瞭解為您在AdobeCloud Manager中的每個程式布建的Git儲存AEM庫。
uuid: 2c42775f-8703-43f7-bad2-7dc086ea9dd7
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: requirements
discoiquuid: f90f0f4c-c1ff-47f6-8d97-ff5018561bf2
feature: 布建
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 2%

---


# 原始碼存放庫 {#source-code-repository}

## Cloud Manager儲存庫{#cloud-manager-repository}

您的[!UICONTROL AEM Managed Services]訂閱將包含由Adobe布建和管理的原始碼儲存庫。 每個客戶的程式都被分配一個唯一的&#x200B;**Git儲存庫** ，在該儲存庫中儲存並保護您的關聯代碼。

作為最佳做法，您應始終使用Cloud Manager的Git儲存庫，該儲存庫為空，不配置任何分支或示例項目。 若要使用Cloud Manager的Git Repository，將會提供&#x200B;**私人存取Token**，讓您使用任何與Git相容的用戶端來建立分支、儲存和擷取代碼、列出提交記錄等。

如需如何在Git中設定分支的詳細資訊，請參閱[設定發行分支](configure-your-release-branches.md)。

有關如何將Cloud Manager的&#x200B;**Git儲存庫**&#x200B;與CI/CD管線一起使用的詳細資訊，請參閱[配置CI/CD管線](configuring-pipeline.md)。

## 內部部署儲存庫{#on-premise-repository}

在某些情況下，您將擁有現有的Git儲存庫，並希望繼續使用它。 在這些情況下，您可以對多個遠程儲存庫使用Git的支援功能。 日常開發將繼續發生在您的Git資料庫中。 當發行分支準備好部署至生產環境時，您會將最新的程式碼推送至Cloud Manager的Git儲存庫，並觸發Cloud Manager CI/CD管道。

>[!NOTE]
>
>要查看常見的Git命令，請參閱[Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)。

