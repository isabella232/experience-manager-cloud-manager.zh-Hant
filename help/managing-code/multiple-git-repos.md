---
title: 使用多個Git儲存庫
description: 不直接使用Cloud Manager的git儲存庫，而是瞭解如何使用您自己的git儲存庫或多個git儲存庫。
exl-id: 53bf78bb-489a-4a83-8459-c361f532d54a
source-git-commit: da9dff997a277c207e2c48207217cb30325f3c0d
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 0%

---

# 使用多個源Git儲存庫 {#working-with-multiple-source-git-repos}

不直接使用Cloud Manager的git儲存庫，而是瞭解如何使用您自己的git儲存庫或多個git儲存庫。

## 同步客戶管理的Git儲存庫 {#syncing-customer-managed-git-repositories}

如果您希望使用您自己的儲存庫或儲存庫，應設定自動同步過程，以確保Cloud Manager的Git儲存庫始終保持最新。

根據您的Git儲存庫的托管位置，可以使用GitHub操作或Jenkins等連續整合解決方案來設定自動化。 在實現自動化後，每次推送到您自己的儲存庫時，都可自動轉發到Cloud Manager的git儲存庫。

雖然單個客戶擁有的Git儲存庫的這種自動化非常簡單，但為多個儲存庫配置此自動化需要更多參與的初始設定。 需要將來自多個Git儲存庫的內容映射到單個Cloud Manager的Git儲存庫中的不同目錄。 需要為Cloud Manager的Git儲存庫設定根Maven `pom.xml`，列出模組部分中的不同子項目

下面是示例 `pom.xml` 用於兩個客戶擁有的git儲存庫。 第一個項目將放入名為 `project-a`，將第二個項目放入名為 `project-b`。

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

這樣的根 `pom.xml` 已推送到Cloud Manager的git儲存庫中的分支。 然後，需要設定這兩個項目以自動將更改轉發到Cloud Manager的git儲存庫。

例如，GitHub操作可以通過向項目A中的分支推送來觸發。該操作將簽出項目A和Cloud Manager git儲存庫，並將項目A的所有內容複製到目錄 `project-a` 在Cloud Manager的Git儲存庫中，然後提交 — 推送更改。

例如， `main` 將項目A中的分支自動推入到 `main` 在Cloud Manager的git儲存庫中分支。 當然，分支之間可能有一個映射，就像向一個名為 `dev` 將項目A中的分支推送到名為 `development` 在Cloud Manager的Git儲存庫中。 項目B需要類似的步驟。

根據分支策略和工作流，可以為不同分支配置同步。 如果使用的Git儲存庫不提供與GitHub操作類似的概念，則也可以通過Jenkins（或類似）進行整合。 在這種情況下，網鈎會觸發Jenkins作業，該作業會執行。

按照以下步驟添加新（第三個）源或儲存庫：

1. 將新GitHub操作添加到新儲存庫，將更改從該儲存庫推送到Cloud Manager的Git儲存庫。
1. 至少執行一次該操作，以確保項目代碼位於Cloud Manager的Git儲存庫中。
1. 在根Maven中添加對新目錄的引用 `pom.xml` 在Cloud Manager git儲存庫中。

## 示例GitHub操作 {#sample-github-action}

這是通過向 `main` 然後將其推入Cloud Manager的git儲存庫的子目錄。 GitHub操作需要提供兩個秘密， `MAIN_USER` 和 `MAIN_PASSWORD`，以便能夠連接並推送到Cloud Manager的git儲存庫。

```java
name: SYNC
env:
  # Username/email used to commit to Cloud Manager's Git repository
  USER_NAME: <NAME>
  USER_EMAIL: <EMAIL>
  # Directory within the Cloud Manager Git repository
  PROJECT_DIR: project-a
  # Cloud Manager's Git repository
  MAIN_REPOSITORY: https://$MAIN_USER:$MAIN_PASSWORD@git.cloudmanager.adobe.com/<PATH>
  # The branch in Cloud Manager's Git repository to push to
  MAIN_BRANCH : <BRANCH_NAME>
 
# Only run on a push to this branch
on:
  push:
     branches: [ main ]
 
jobs:
  build:
    runs-on: ubuntu-latest
 
    steps:
      # Checkout this project into a sub folder
      - uses: actions/checkout@v2
        with:
          path: sub
      # Cleanup sub project
      - name: Clean project
        run: |
          git -C sub log --format="%an : %s" -n 1 > commit.txt
          rm -rf sub/.git
          rm -rf sub/.github
      # Set global git configuration
      - name: Set git config
        run: |
          git config --global credential.helper cache
          git config --global user.email ${USER_EMAIL}
          git config --global user.name ${USER_NAME}
      # Checkout the main project
      - name: Checkout main project
        run:
          git clone -b ${MAIN_BRANCH} https://${{ secrets.PAT }}@github.com/${MAIN_REPOSITORY}.git main 
      # Move sub project
      - name: Move project to main project
        run: |
          rm -rf main/${PROJECT_DIR} 
          mv sub main/${PROJECT_DIR}
      - name: Commit Changes
        run: |
          git -C main add -f ${PROJECT_DIR}
          git -C main commit -F ../commit.txt
          git -C main push
```

如上所示，使用GitHub操作非常靈活。 可以執行Git儲存庫分支之間的任何映射以及將單獨的Git項目映射到主項目的目錄佈局中的任何映射。

>[!NOTE]
>
>上述指令碼使用 `git add` 更新假定包含刪除的儲存庫。 根據Git的預設配置，可能需要用 `git add --all`。

## 示例Jenkins作業 {#sample-jenkins-job}

這是一個示例指令碼，可用於Jenkins作業或類似操作。 它由Git儲存庫中的更改觸發。 Jenkins作業將檢查該項目或分支的最新狀態，然後觸發此指令碼。

此指令碼將檢出Cloud Manager的git儲存庫，並將項目代碼提交到子目錄。

詹金斯的工作需要有兩個秘密， `MAIN_USER` 和 `MAIN_PASSWORD`，以便能夠連接並推送到Cloud Manager的git儲存庫。

```java
# Username/email used to commit to Cloud Manager's Git repository
export USER_NAME=<NAME>
export USER_EMAIL=<EMAIL>
# Directory within the Cloud Manager Git repository
export PROJECT_DIR=project-a
# Cloud Manager's Git repository
export MAIN_REPOSITORY=https://$MAIN_USER:$MAIN_PASSWORD@git.cloudmanager.adobe.com/<PATH>
# The branch in Cloud Manager's Git repository to push to
export MAIN_BRANCH=<BRANCH_NAME>
 
# clean up and init
rm -rf target
mkdir target
 
# mv project to sub folder
mkdir target/sub
for f in .* *
do
    if [ "$f" != "." -a "$f" != ".." -a "$f" != "target" ]
    then
        mv "$f" target/sub
    fi
done
cd target
 
# capture log and remove git info
cd sub
git log --format="%an : %s" -n 1 > ../commit.txt
rm -rf .git
rm -rf .github
cd ..
 
# checkout main repository
git clone -b $MAIN_BRANCH $MAIN_REPOSITORY main
cd main
 
# configure main repository
git config credential.helper cache
git config user.email $USER_EMAIL
git config user.name $USER_NAME
 
# update project in main
rm -rf $PROJECT_DIR
mv ../sub $PROJECT_DIR
 
# commit changes to main
git add -f $PROJECT_DIR
git commit -F ../commit.txt
git push
```

如上所示，使用Jenkins工作非常靈活。 可以執行Git儲存庫分支之間的任何映射以及將單獨的Git項目映射到主項目的目錄佈局中的任何映射。

>[!NOTE]
>
>上述指令碼使用 `git add` 更新假定包含刪除的儲存庫。根據git的預設配置，可能需要用 `git add --all`。
