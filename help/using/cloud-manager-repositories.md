---
title: Cloud Manager資料庫
description: Cloud Manager資料庫
exl-id: 384b197d-f7a7-4022-9b16-9d83ab788966
source-git-commit: 280d760766cf445e609b865f827c01b4ab1db69c
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---

# Cloud Manager資料庫 {#cloud-manager-repos}

可以通過「儲存庫」頁查看和管理在Cloud Manager中建立和可用的儲存庫。

## 添加和管理儲存庫 {#add-manage-repos}

按照以下步驟查看和管理Cloud Manager中的儲存庫：

1. 從 **計畫概述** ，按一下 **儲存庫** 頁籤並導航至 **儲存庫** 的子菜單。

1. 按一下 **添加儲存庫** 的子菜單。

   >[!NOTE]
   >必須登錄部署管理器或業務所有者角色中的用戶才能添加儲存庫。

   ![](assets/create-repo2.png)


1. 根據請求輸入名稱和說明，然後按一下 **保存**。

   ![](assets/repo-1.png)

1. 選擇 **保存**。 新建立的回購將顯示在表中，如下所示。

   ![](assets/create-repo3.png)

   >[!NOTE]
   >在Cloud Manager中建立的儲存庫也將可供您在添加或編輯管道步驟期間選擇。

1. 您可以選擇儲存庫，然後按一下表最右側的菜單選項 **複製儲存庫URL**。 **查看和更新** 或 **刪除** 如下圖所示，

   ![](assets/create-repo3.png)



## Git子模組支援 {#git-submodule-support}

Git子模組可用於在生成時合併多個分支在Git儲存庫中的內容。 當Cloud Manager的生成進程執行時，在克隆了為管道配置的儲存庫並簽出了已配置的分支後，如果分支包含 `.gitmodules` 檔案，執行命令。

```
$ git submodule update --init
```

這會將每個子模組檢出到相應的目錄中。 這種技術是 [使用多個源Git儲存庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/working-with-multiple-source-git-repos.html) 對於那些願意使用git子模組且不想管理外部合併進程的組織。

例如，假設有三個儲存庫，每個儲存庫都包含一個名為main的分支。 在「主」儲存庫中，即在管道中配置的儲存庫中，主分支有一個pom.xml檔案，聲明其他兩個儲存庫中包含的項目：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
   
    <groupId>customer.group.id</groupId>
    <artifactId>customer-reactor</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <packaging>pom</packaging>
   
    <modules>
        <module>project-a</module>
        <module>project-b</module>
    </modules>
   
</project>
```

然後，您將為另外兩個儲存庫添加子模組：

```
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectA/ project-a
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectB/ project-b
```

這將導致 `.gitmodules` 檔案如下所示：

```
[submodule "project-a"]
    path = project-a
    url = https://git.cloudmanager.adobe.com/ProgramName/projectA/
    branch = main
[submodule "project-b"]
    path = project-b
    url = https://git.cloudmanager.adobe.com/ProgramName/projectB/
    branch = main
```

有關git子模組的詳細資訊，請參閱 [Git參考手冊](https://git-scm.com/book/en/v2/Git-Tools-Submodules)。

使用git子模組時，請記住以下事項：

* Git URL必須完全按上述語法進行。 出於安全原因，請勿在這些URL中嵌入憑據。
* 只支援分支根上的子模組。
* 將Git子模組引用儲存到特定的Git提交。 因此，當對子模組儲存庫進行更改時，需要更新引用的提交，例如，使用 `git submodule update --remote`。
* 除非有其他必要，強烈建議使用「淺」子模組。 要執行此操作，請運行 `git config -f .gitmodules submodule.<submodule path>.shallow true` 每個子模組。
