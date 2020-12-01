---
title: 設定您的發行分支
seo-title: 設定您的發行分支
description: 在Git中為AEM Cloud Manager設定發行分支
seo-description: 請依照本頁瞭解如何以git設定發行分支。
uuid: d12a8b85-b7fd-4b55-a05a-a0f874ce598c
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: getting-started
discoiquuid: 53807ea6-9464-429d-9322-85c9f405dff6
translation-type: tm+mt
source-git-commit: 9c0df236c1e800802d62dea09996bb8e1e7033f7
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 3%

---


# 設定您的發行分支 {#configure-your-release-branches}

## 以Git {#setting-up-your-first-branch-in-git}設定您的第一個分支

為Cloud Manager中已登錄的每個程式布建一個&#x200B;**Git儲存庫**，該儲存庫最初為空。 此儲存庫可以包含與您的開發流程一樣多（或更少）的分支，但至少必須有一個分支，CI/CD管道使用該分支將應用程式碼部署到舞台和生產環境。 最佳做法是使用`master`作為此分支的名稱。 方便的是，這是Git客戶在設定新專案時的預設行為。

例如，在設定新項目時，您將運行一組類似以下命令：

```shell
$ git init
Initialized empty Git repository in /Users/myname/workspace/new-project/.git/
... steps which add Maven build files and source code ...
$ git add pom.xml core/pom.xml core/src ui.apps/pom.xml ui.apps/src
$ git commit -m "initial commit"
 19 files changed, 777 insertions(+)
 create mode 100644 core/pom.xml
 create mode 100644 pom.xml
 create mode 100644 ui.apps/pom.xml
 create mode 100644 ui.apps/src/main/content/META-INF/vault/config.xml
 create mode 100644 ui.apps/src/main/content/META-INF/vault/definition/.content.xml
 create mode 100644 ui.apps/src/main/content/META-INF/vault/filter.xml
 create mode 100644 ui.apps/src/main/content/META-INF/vault/nodetypes.cnd
 create mode 100644 ui.apps/src/main/content/META-INF/vault/properties.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/apps/my-aem-project/install/.vltignore
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/.content.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/.content.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/settings/.content.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/settings/wcm/.content.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/settings/wcm/policies/.content.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/settings/wcm/policies/_rep_policy.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/settings/wcm/template-types/.content.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/settings/wcm/template-types/_rep_policy.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/settings/wcm/templates/.content.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/settings/wcm/templates/_rep_policy.xml
```

>[!NOTE]
>
>它不需要使用命令行客戶端。 有多種圖形化Git用戶端可做為獨立應用程式或整合開發環境(IDE)的一部分，例如Eclipse或IntelliJ。 只要用戶端應用程式支援使用HTTPS的Git，就應與[!UICONTROL Cloud Manager]相容。

## 推送您的第一個分支{#pushing-your-first-branch}

在您至少提交一個修訂版本後，可以將[!UICONTROL Cloud Manager]儲存庫添加為&#x200B;**remote** ，然後將提交推送到該儲存庫：

```shell
$ git remote add adobe <url>
$ git push adobe master
Counting objects: 36, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (27/27), done.
Writing objects: 100% (36/36), 7.31 KiB | 1.83 MiB/s, done.
Total 36 (delta 6), reused 0 (delta 0)
To <url>
 * [new branch]      master -> master
```

>[!NOTE]
>
>在[!UICONTROL Cloud Manager]上線期間，客戶成功工程部門將會為您提供特定URL以及您的認證。

## 其他分支{#additional-branches}

單一`master`分支可以滿足非常簡單的專案，但在大多數情況下，需要更複雜的分支策略。 許多客戶遵循的流程是，在名為`develop`的分支上執行日常開發活動，而開發分支在部署時合併到`master`分支。

>[!NOTE]
>
>要查看常用的git命令，請參閱[Git Cheat Sheet](https://github.github.com/training-kit/downloads/github-git-cheat-sheet)。
