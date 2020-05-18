---
title: Maven 專案版本處理
seo-title: Maven 專案版本處理
description: 進一步瞭解Maven Project Version Handling。
seo-description: 請依照本頁進一步瞭解Maven專案版本處理。
translation-type: tm+mt
source-git-commit: e2187565e7f06d64841eb2af9b4b1a56feb5ebe4
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 7%

---


# Maven 專案版本處理 {#project-version}

## Understanding Maven Project Version Handling {#understanding-project-version}

對於舞台和生產部署，Cloud Manager會產生獨特的遞增版本。

此版本在管線執行詳細資料頁面和活動頁面上顯示。 當執行建置時，Maven專案會更新為使用此版本，並在git儲存庫中建立標籤，其名稱為該版本。

如果原始專案版本符合特定標準，更新的Maven專案版本將合併原始專案版本和Cloud Manager產生的版本。 但是，標籤一律會使用產生的版本。 要進行此合併，原始項目版本必須由三個版本段組成，例如1.0.0或1.2.3，但不是1.0或1，且原始版本不得以-SNAPSHOT結束。

如果原始版本符合此標準，則產生的版本會附加至原始版本，做為新版本區段。 產生的版本也會稍作修改，以包含正確的排序和版本處理。 例如，假設生成的版本為2019.926.121356.0000020490:

| **版本** | **pom.xml中的版本** | **評論** |
|---|---|---|
| 1.0.0 | 1.0.0.2019_0926_121356_0000020490 | 格式正確的原始版本 |
| 1.0.0-快照 | 2019.926.121356.0000020490 | 快照版本，已覆寫 |
| 1 | 2019.926.121356.0000020490 | 不完整版本，已覆寫 |

>[!NOTE]
>
>無論原始版本是否已併入Cloud Manager初始化的版本，原始版本都可作為名為cloudManagerOriginalVersion的Maven屬 *性使用。*
