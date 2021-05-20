---
title: 設定您的發行分支
seo-title: 設定您的發行分支
description: 在Git中設定AEM Cloud Manager的發行分支
seo-description: 請詳閱本頁，了解如何在Git中設定發行分支。
uuid: d12a8b85-b7fd-4b55-a05a-a0f874ce598c
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: getting-started
discoiquuid: 53807ea6-9464-429d-9322-85c9f405dff6
feature: Git存放庫
exl-id: ff2ae28f-902e-4fb2-aeb1-3636cb5cd9bb
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 3%

---

# 設定您的發行分支 {#configure-your-release-branches}

## 在Git {#setting-up-your-first-branch-in-git}中設定第一個分支

針對在Cloud Manager中上線的每個程式，布建一個原本空白的&#x200B;**Git存放庫**。 此存放庫可包含您開發程式遵循的分支數量（或數量不多），但CI/CD管道必須至少使用一個分支，才能將應用程式程式碼部署至預備和生產環境。 最佳做法是使用`master`作為此分支的名稱。 設定新專案時，這是Git用戶端的預設行為。

例如，在設定新項目時，您將運行一組命令，如：

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
>它不需要使用命令行客戶端。 提供多種圖形化Git用戶端，可作為獨立應用程式或整合開發環境(IDE)的一部分，例如Eclipse或IntelliJ。 只要用戶端應用程式使用HTTPS支援Git，就應與[!UICONTROL Cloud Manager]相容。

## 推送第一個分支{#pushing-your-first-branch}

在您至少提交了一個修訂版本後，可以將[!UICONTROL Cloud Manager]儲存庫添加為&#x200B;**remote**，然後將提交推送到它：

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
>在[!UICONTROL Cloud Manager]上線期間，客戶成功工程將會提供特定URL及您的認證給您。

## 其他分支{#additional-branches}

單個`master`分支可以滿足非常簡單的項目，但在大多數情況下，需要更複雜的分支策略。 許多客戶會遵循在名為`develop`的分支上執行日常開發活動的程式，而開發分支在需要部署時會合併至`master`分支。

>[!NOTE]
>
>若要檢視常見的git命令，請參閱[ Git速查表](https://github.github.com/training-kit/downloads/github-git-cheat-sheet)。
