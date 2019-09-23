---
title: 原始碼儲存庫
seo-title: Adobe AEM Cloud manager的原始碼儲存庫
description: 請依照本頁瞭解為Cloud manager中的每個程式布建的git儲存庫。
seo-description: 請依照本頁瞭解為Adobe AEM Cloud manager中每個程式布建的Git儲存庫。
uuid: 2c42775f-8703-43f7-bad2-7dc086ea9dd7
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: 需求
discoiquuid: f90f0f4c-c1ff-47f6-8d97-ff5018561bf2
translation-type: tm+mt
source-git-commit: 697311cd00ef96568f6befd2fe76febafc27961e

---


# 原始碼儲存庫 {#source-code-repository}

## Cloud Manager資料庫 {#cloud-manager-repository}

您的 [!UICONTROL AEM Managed Services] 訂閱將包含由Adobe布建和管理的原始碼儲存庫。 每個客戶的程式都被指派一個唯一的 **Git儲存庫**，在該儲存庫中儲存並保護您的關聯代碼。

作為最佳做法，您應始終使用Cloud manager的Git儲存庫，該儲存庫為空，不配置任何分支或示例項目。 若要使用Cloud manager的Git Repository，您將會獲得一個私用存取Token **** ，可讓您使用任何與Git相容的用戶端來建立分支、儲存和擷取您的程式碼、列出提交記錄等。

如需如何在Git中設定分支的詳細資訊，請參 [閱設定發行分支](configure-your-release-branches.md)。

有關如何將Cloud Manager的 **Git儲存庫與CI/CD管道一起使用的詳細資訊** ，請參 [閱配置CI/CD管道](configuring-pipeline.md)。

## 內部部署儲存庫 {#on-premise-repository}

在某些情況下，您將擁有現有的Git儲存庫，並希望繼續使用它。 在這些情況下，您可以對多個遠程儲存庫使用Git的支援功能。 日常開發將繼續發生在您的Git資料庫中。 當發行分支準備好部署至生產環境時，您會將最新的程式碼推送至Cloud Manager的Git儲存庫，並觸發Cloud Manager CI/CD管道。

>[!NOTE]
>
>若要檢視常用的Git指令，請參閱 [Git快速參考表](https://education.github.com/git-cheat-sheet-education.pdf)。

