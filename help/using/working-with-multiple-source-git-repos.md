---
title: 使用多源Git儲存庫
description: 使用多源Git儲存庫- Cloud Manager
feature: Git Repositories
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 0%

---


# 使用多源Git儲存庫{#working-with-multiple-source-git-repos}


## 同步客戶管理的Git儲存庫{#syncing-customer-managed-git-repositories}

客戶可以使用自己的Git儲存庫或多個自己的Git儲存庫，而不是直接使用Cloud Manager的Git儲存庫。 在這些情況下，應設定自動同步過程，以確保Cloud Manager的Git儲存庫始終保持最新狀態。 根據客戶的Git儲存庫的托管位置，可以使用GitHub操作或像Jenkins這樣的連續整合解決方案來設定自動化。 有了自動功能，每個推送至客戶擁有的Git儲存庫的推送都會自動轉送至Cloud Manager的Git儲存庫。

雖然單個客戶擁有的Git儲存庫的這種自動化功能是直接進行的，但為多個儲存庫設定此功能需要初始設定。 來自多個Git儲存庫的內容必須映射到單個Cloud Manager的Git儲存庫中的不同目錄。  Cloud Manager的Git儲存庫需要配置一個根Maven pom，在模組部分列出不同的子項目

以下是兩個客戶擁有的Git儲存庫的示例pom:第一個項目將被放入名為`project-a`的目錄中，第二個項目將被放入名為`project-b`的目錄中。

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

此類根pom被推送到Cloud Manager的Git儲存庫中的分支。 然後，需要設定這兩個項目，以自動將更改轉發到Cloud Manager的Git儲存庫。

例如，GitHub動作可透過推播至專案A中的分支來觸發。該操作將簽出項目A和Cloud Manager Git儲存庫，並將項目A的所有內容複製到Cloud Manager Git儲存庫中的`project-a`目錄，然後提交推送更改。 例如，專案A中主分支的變更會自動推送至Cloud Manager的git儲存庫中的主分支。 當然，分支之間可能會有對應，例如推播至專案A中名為「dev」的分支，會推送至Cloud Manager Git儲存庫中名為「development」的分支。 項目B需要類似的步驟。

可針對不同的分支設定同步，視分支策略和工作流程而定。 如果使用的Git儲存庫沒有提供類似GitHub操作的概念，則也可以通過Jenkins（或類似）進行整合。 在這種情況下，網路鈎會觸發Jenkins作業，該作業負責。

按照以下步驟添加新的（第三個）源或儲存庫：

1. 將新的GitHub操作添加到新儲存庫，將該儲存庫中的更改推送到Cloud Manager的Git儲存庫。
1. 請至少執行一次該動作，以確保專案代碼位於Cloud Manager的Git Repository中。
1. 在Cloud Manager Git儲存庫的根Maven pom中添加對新目錄的引用。


## GitHub動作範例{#sample-github-action}

這是GitHub動作的範例，是透過推送至主分支，然後推送至Cloud Manager Git Repository的子目錄而觸發。 GitHub操作需要提供`MAIN_USER`和`MAIN_PASSWORD`兩個機密，才能連接並推送到Cloud Manager的Git儲存庫。

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

如上所示，使用GitHub動作非常有彈性。 可以執行Git儲存庫分支之間的任何映射，以及將單獨的git項目映射到主項目的目錄佈局中的任何映射。

>[!NOTE]
>上述指令碼使用`git add`更新假定包含刪除的儲存庫——根據Git的預設配置，這需要替換為`git add --all`。

## 示例Jenkins Job {#sample-jenkins-job}

此指令碼示例可用於Jenkins作業或類似作業。 它由Git儲存庫中的更改觸發。 Jenkins作業會檢查該項目或分支的最新狀態，然後觸發此指令碼。

此指令碼隨後會簽出Cloud Manager的Git儲存庫，並將項目代碼提交到子目錄。

Jenkins作業需要提供`MAIN_USER`和`MAIN_PASSWORD`兩個秘密，才能連接並推送到Cloud Manager的Git儲存庫。

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

如上所示，使用Jenkins工作非常靈活。 可以執行Git儲存庫分支之間的任何映射，以及將單獨的Git項目映射到主項目的目錄佈局中的任何映射。

>[!NOTE]
>上述指令碼使用`git add`更新假定包含刪除的儲存庫——根據Git的預設配置，這需要替換為`git add --all`。