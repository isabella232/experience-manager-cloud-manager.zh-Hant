---
title: 原始碼存放庫
seo-title: Adobe AEM Cloud Manager的原始碼存放庫
description: 請依照此頁面瞭解您在Cloud Manager中每個程式布建的git存放庫。
seo-description: 請依照此頁面瞭解您在Adobe AEM Cloud Manager中每個程式布建的git存放庫。
uuid: 2c42775f-8703-43f7-壞事2-7dc086ea9d7
contentOwner: jsyal
products: SG_ PERIENCENCENAGER/CLUDManager
topic-tags: 需求
discoiquuid: f90f0f4c-c1 ff-47f6-8d97-ff5018561 bc2
translation-type: tm+mt
source-git-commit: 1dfb065c09569f811e5a006d3d74825d3bd7cc8d

---


# 原始碼存放庫 {#source-code-repository}

## Cloud Manager存放庫 {#cloud-manager-repository}

[!UICONTROL AEM Managed Services] 您的訂閱將包含由Adobe布建並管理的原始碼存放庫。每個客戶的計劃都會被指派一個獨特 **的獨特Git存放庫**，您的相關代碼將會儲存和安全。

作為最佳實務，您應一律使用Cloud Manager的Git存放庫，此存放庫不會設定任何分支或範例專案。若要使用Cloud Manager的Git儲存庫，將會提供 **私人存取Token的私人存取Token** ，讓您使用任何Git相容用戶端建立分支、儲存和擷取您的程式碼、列出提交記錄等。

如需如何在Git中設定分支的詳細資訊，請參閱 [設定您的版本分支](configure-your-release-branches.md)。

如需如何使用雲端管理員 **的Git儲存庫** 搭配CI/CD管線的詳細資訊，請參閱 [設定您的CI/CD管線](configuring-pipeline.md)。

## 內部部署儲存庫 {#on-premise-repository}

在某些情況下，您將擁有現有的Git存放庫並想要繼續使用它。在這種情況下，您可以針對多個遠端儲存庫使用Git的支援功能。每日開發的開發將繼續發生在您的Git存放庫中。當發行分支已準備好進行部署時，您會將最新程式碼推送至Cloud Manager的Git儲存庫，並觸發Cloud Manager CI/CD管線。

>[!NOTE]
>
>若要檢視常用Git命令，請參閱 [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)。

