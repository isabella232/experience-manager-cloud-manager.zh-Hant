---
title: Dispatcher 設定
description: 了解如何使用 Cloud Manager 部署 Dispatcher 設定檔案。
exl-id: ffc2b60e-bde7-48ca-b268-dea0f8fd4e30
source-git-commit: 6572c16aea2c5d2d1032ca5b0f5d75ade65c3a19
workflow-type: ht
source-wordcount: '0'
ht-degree: 100%

---


# Dispatcher 設定 {#manage-your-dispatcher-configurations}

了解如何使用 Cloud Manager 部署 Dispatcher 設定檔案。 

## 使用 Cloud Manager 部署 Dispatcher 設定 {#deploying-dispatcher-configurations}

Cloud Manager 能夠部署 Web 伺服器和 Dispatcher 設定檔案的前提在於它們會和一般 AEM 內容套件一起儲存在 Git 存放庫中。

若要利用此功能，Maven 組建應產生 .zip 檔案，且其中至少包含兩個目錄：`conf` 和 `conf.d`。 可使用 `maven-assembly-plugin` 產生此 .zip 檔案。

Cloud Manager 使用內建[專案建立精靈](/help/getting-started/using-the-wizard.md)產生的專案具有自動建立的正確 Maven 專案結構。如果您才剛使用 Adobe Managed Services (AMS)，這是建立的路徑。

部署到 Dispatcher 執行個體後，Dispatcher 執行個體上的這些目錄的內容將被您的 Git 存放庫中的內容覆寫。由於 Web 伺服器和 Dispatcher 設定檔案經常需要環境特定資訊才能正確使用此功能，因此您首先需要和客戶成功工程師 (CSE) 一起將這些環境變數設定為 `/etc/sysconfig/httpd`。

## 現有受管理服務客戶的 Dispatcher 設定 {#steps-for-configuring-dispatcher}

請依照下列這些步驟，完成初始的 Dispatcher 設定。

1. 向您的 CSE 獲取最新的生產設定檔案。
1. 移除硬式編碼的環境特定資料，例如發佈轉譯器 IP，並以變數取代。
1. 在每個目標 Dispatcher 的索引碼值配對中定義所需的變數，並要求您的 CSE 將這些變數新增到每個執行個體上的 `/etc/sysconfig/httpd`。
1. 在中繼環境中測試更新的設定。
1. 測試後，請要求您的 CSE 部署到生產環境。
1. 將檔案提交到您的 Git 存放庫。
1. 透過 Cloud Manager 部署。

>[!NOTE]
>
>將 Dispatcher 和 Web 伺服器設定遷移到您的 Git 存放庫可以在 Cloud Manager 上線期間完成，但也可以在以後的某個時間點完成。

### 範例 {#example}

特定的檔案和目錄結構可能會依您專案的特定情況而有所不同，但本範例應可提供具體的指南，說明如何建構您的專案以包含 Apache 和 Dispatcher 設定。

1. 建立名為 `dispatcher` 的子目錄。

   您可以在此處使用任何名稱，但在此步驟中建立的目錄名稱必須和步驟 6 中使用的名稱相同。

1. 該子目錄將包含一個 Maven 模組，該模組會使用 Maven 組裝外掛程式來建置 Dispatcher .zip 檔案。若要開始進行，可在 `dispatcher` 目錄中，建立包含此內容的 `pom.xml` 檔案，在必要時變更 `parent` 參照、`artifactId` 和 `name`。

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <project xmlns="http://maven.apache.org/POM/4.0.0"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
       <modelVersion>4.0.0</modelVersion>
       <parent>
           <!-- reference to your parent pom -->
       </parent>
   
       <artifactId>dispatcher</artifactId> <!-- feel free to change this -->
       <packaging>pom</packaging>
       <name>dispatcher</name> <!-- feel free to change this -->
   
       <build>
           <plugins>
               <plugin>
                   <groupId>org.apache.maven.plugins</groupId>
                   <artifactId>maven-assembly-plugin</artifactId>
                   <version>3.1.0</version>
                   <executions>
                       <execution>
                           <phase>package</phase>
                           <goals><goal>single</goal></goals>
                           <configuration>
                               <descriptors>
                                   <descriptor>assembly.xml</descriptor>
                               </descriptors>
                               <appendAssemblyId>false</appendAssemblyId>
                           </configuration>
                       </execution>
                   </executions>
               </plugin>
           </plugins>
       </build>
   </project>
   ```

   * 和步驟 1 一樣，如果需要，此處的 artifactId 和 name 可以是其他值。`dispatcher` 在此僅用為範例。

1. 此 Maven 組裝外掛程式需要 `descriptor` 來定義建立 .zip 檔案的方式。若要建立此描述項，可在包含以下內容的 `dispatcher` 子目錄 (名為 `assembly.xml`) 中建立檔案。請注意，在上述 `pom.xml` 檔案的第 26 行會參照此檔案名稱。

   ```xml
   <assembly xmlns="http://maven.apache.org/ASSEMBLY/2.0.0"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://maven.apache.org/ASSEMBLY/2.0.0 http://maven.apache.org/xsd/assembly-2.0.0.xsd">
     <id>distribution</id>
     <formats>
       <format>zip</format>
     </formats>
     <includeBaseDirectory>false</includeBaseDirectory>
     <fileSets>
       <fileSet>
         <directory>${basedir}/src</directory>
         <includes>
           <include>**/*</include>
         </includes>
         <outputDirectory></outputDirectory>
       </fileSet>
     </fileSets>
   </assembly>
   ```

1. 在 Dispatcher 子目錄中建立一個名為 `src` 的子目錄 (如上述第 11 行組裝描述項中提及的)，以儲存實際的 Apache 和 Dispatcher 設定。在此 `src` 目錄中，建立名為 `conf`、`conf.d`、`conf.dispatcher.d` 和 `conf.modules.d` 的目錄。

1. 以您的設定檔案填入 `conf`、`conf.d`、`conf.dispatcher.d` 和 `conf.modules.d` 目錄。例如，預設的設定會由這些檔案和符號連結組成。

   ```
   dispatcher
   ├── assembly.xml
   ├── pom.xml
   └── src
       ├── conf
       │  ├── httpd.conf
       │  └── magic
       ├── conf.d
       │  ├── README
       │  ├── autoindex.conf
       │  ├── available_vhosts
       │  │  ├── aem_author.vhost
       │  │  ├── aem_flush.vhost
       │  │  ├── aem_health.vhost
       │  │  ├── aem_lc.vhost
       │  │  └── aem_publish.vhost
       │  ├── dispatcher_vhost.conf
       │  ├── enabled_vhosts
       │  │  ├── aem_author.vhost -> ../available_vhosts/aem_author.vhost
       │  │  ├── aem_flush.vhost -> ../available_vhosts/aem_flush.vhost
       │  │  └── aem_publish.vhost -> ../available_vhosts/aem_publish.vhost
       │  ├── rewrites
       │  │  ├── base_rewrite.rules
       │  │  └── xforwarded_forcessl_rewrite.rules
       │  ├── userdir.conf
       │  ├── variables
       │  │  └── ams_default.vars
       │  ├── welcome.conf
       │  └── whitelists
       │      └── 000_base_whitelist.rules
       ├── conf.dispatcher.d
       │  ├── available_farms
       │  │  ├── 000_ams_author_farm.any
       │  │  ├── 001_ams_lc_farm.any
       │  │  └── 999_ams_publish_farm.any
       │  ├── cache
       │  │  ├── ams_author_cache.any
       │  │  ├── ams_author_invalidate_allowed.any
       │  │  ├── ams_publish_cache.any
       │  │  └── ams_publish_invalidate_allowed.any
       │  ├── clientheaders
       │  │  ├── ams_author_clientheaders.any
       │  │  ├── ams_common_clientheaders.any
       │  │  ├── ams_lc_clientheaders.any
       │  │  └── ams_publish_clientheaders.any
       │  ├── dispatcher.any
       │  ├── enabled_farms
       │  │  ├── 000_ams_author_farm.any -> ../available_farms/000_ams_author_farm.any
       │  │  └── 999_ams_publish_farm.any -> ../available_farms/999_ams_publish_farm.any
       │  ├── filters
       │  │  ├── ams_author_filters.any
       │  │  ├── ams_lc_filters.any
       │  │  └── ams_publish_filters.any
       │  ├── renders
       │  │  ├── ams_author_renders.any
       │  │  ├── ams_lc_renders.any
       │  │  └── ams_publish_renders.any
       │  └── vhosts
       │      ├── ams_author_vhosts.any
       │      ├── ams_lc_vhosts.any
       │      └── ams_publish_vhosts.any
       └── conf.modules.d
           ├── 00-base.conf
           ├── 00-dav.conf
           ├── 00-lua.conf
           ├── 00-mpm.conf
           ├── 00-proxy.conf
           ├── 00-systemd.conf
           ├── 01-cgi.conf
           └── 02-dispatcher.conf
   ```

1. 最後，請在專案根目錄中的 `pom.xml` 檔案中，新增 `<module>` 元素，以包含 Dispatcher 模組。

   例如，如果您現有的模組清單為

   ```xml
       <modules>
           <module>core</module>
           <module>ui.apps</module>
           <module>ui.content</module>
       </modules>
   ```

   您應該將其變更為

   ```xml
       <modules>
           <module>core</module>
           <module>ui.apps</module>
           <module>ui.content</module>
           <module>dispatcher</module>
       </modules>
   ```

   * 如步驟 1 中所述，`<module>` 元素的值必須和已建立的目錄名稱相符。

1. 若要進行測試，請在專案根目錄中執行 `mvn clean package`。您應該在輸出中看到類似這樣的行。

   ```
   [INFO] --- maven-assembly-plugin:3.1.0:single (default) @ dispatcher ---
   [INFO] Reading assembly descriptor: assembly.xml
   [INFO] Building zip: /Users/me/mycompany/dispatcher/target/dispatcher-1.0-SNAPSHOT.zip
   ```

   您還可以解壓縮此檔案以檢視其內容。

   ```shell
   $ unzip -l dispatcher/target/dispatcher-1.0-SNAPSHOT.zip
   Archive:  dispatcher/target/dispatcher-1.0-SNAPSHOT.zip
     Length      Date    Time    Name
   ---------  ---------- -----   ----
           0  09-12-2018 12:53   conf.modules.d/
           0  10-19-2018 10:38   conf.dispatcher.d/
           0  09-12-2018 12:53   conf.dispatcher.d/available_farms/
           0  09-12-2018 12:53   conf.dispatcher.d/filters/
           0  09-12-2018 12:53   conf.dispatcher.d/renders/
           0  09-12-2018 12:53   conf.dispatcher.d/cache/
           0  09-12-2018 12:53   conf.dispatcher.d/clientheaders/
           0  09-12-2018 12:53   conf.dispatcher.d/enabled_farms/
           0  09-12-2018 12:53   conf.dispatcher.d/vhosts/
           0  09-12-2018 12:53   conf.d/
           0  09-12-2018 12:53   conf.d/rewrites/
           0  09-12-2018 12:53   conf.d/whitelists/
           0  09-12-2018 12:53   conf.d/variables/
           0  11-01-2018 13:53   conf.d/enabled_vhosts/
           0  09-12-2018 12:53   conf.d/available_vhosts/
           0  09-12-2018 12:53   conf/
          88  09-12-2018 12:53   conf.modules.d/00-systemd.conf
        4913  09-12-2018 12:53   conf.dispatcher.d/available_farms/999_ams_publish_farm.any
         152  09-12-2018 12:53   conf.dispatcher.d/renders/ams_lc_renders.any
         490  09-12-2018 12:53   conf.dispatcher.d/clientheaders/ams_common_clientheaders.any
        1727  09-12-2018 12:53   conf.d/rewrites/base_rewrite.rules
          36  09-12-2018 12:53   conf.d/enabled_vhosts/aem_author.vhost
       11753  09-12-2018 12:53   conf/httpd.conf
         957  09-12-2018 12:53   conf.modules.d/00-proxy.conf
         944  09-12-2018 12:53   conf.dispatcher.d/available_farms/001_ams_lc_farm.any
         220  09-12-2018 12:53   conf.dispatcher.d/cache/ams_author_invalidate_allowed.any
          43  09-12-2018 12:53   conf.dispatcher.d/enabled_farms/999_ams_publish_farm.any
         516  09-12-2018 12:53   conf.d/welcome.conf
          37  09-12-2018 12:53   conf.d/enabled_vhosts/aem_publish.vhost
       13077  09-12-2018 12:53   conf/magic
          96  09-12-2018 12:53   conf.modules.d/02-dispatcher.conf
        2601  09-12-2018 12:53   conf.dispatcher.d/available_farms/000_ams_author_farm.any
         837  09-12-2018 12:53   conf.dispatcher.d/cache/ams_author_cache.any
          42  09-12-2018 12:53   conf.dispatcher.d/enabled_farms/000_ams_author_farm.any
        2926  09-12-2018 12:53   conf.d/autoindex.conf
        2555  09-12-2018 12:53   conf.d/available_vhosts/aem_lc.vhost
          41  09-12-2018 12:53   conf.modules.d/00-lua.conf
        2234  09-12-2018 12:53   conf.dispatcher.d/filters/ams_publish_filters.any
         220  09-12-2018 12:53   conf.dispatcher.d/cache/ams_publish_invalidate_allowed.any
         402  09-12-2018 12:53   conf.dispatcher.d/dispatcher.any
         573  09-12-2018 12:53   conf.d/whitelists/000_base_whitelist.rules
         871  09-12-2018 12:53   conf.d/available_vhosts/aem_flush.vhost
         139  09-12-2018 12:53   conf.modules.d/00-dav.conf
         742  09-12-2018 12:53   conf.dispatcher.d/filters/ams_author_filters.any
         557  09-12-2018 12:53   conf.dispatcher.d/cache/ams_publish_cache.any
         105  09-12-2018 12:53   conf.dispatcher.d/vhosts/ams_lc_vhosts.any
         101  09-12-2018 12:53   conf.dispatcher.d/vhosts/ams_publish_vhosts.any
        3582  09-12-2018 12:53   conf.d/dispatcher_vhost.conf
        2529  09-12-2018 12:53   conf.d/available_vhosts/aem_publish.vhost
         742  09-12-2018 12:53   conf.modules.d/00-mpm.conf
          88  09-12-2018 12:53   conf.dispatcher.d/filters/ams_lc_filters.any
         177  09-12-2018 12:53   conf.dispatcher.d/clientheaders/ams_lc_clientheaders.any
         366  09-12-2018 12:53   conf.d/README
        2723  09-12-2018 12:53   conf.d/available_vhosts/aem_author.vhost
        3739  09-12-2018 12:53   conf.modules.d/00-base.conf
         138  09-12-2018 12:53   conf.dispatcher.d/renders/ams_author_renders.any
          44  09-12-2018 12:53   conf.dispatcher.d/clientheaders/ams_publish_clientheaders.any
         112  09-12-2018 12:53   conf.dispatcher.d/vhosts/ams_author_vhosts.any
         580  09-12-2018 12:53   conf.d/variables/ams_default.vars
          35  09-12-2018 12:53   conf.d/enabled_vhosts/aem_flush.vhost
        1252  09-12-2018 12:53   conf.d/userdir.conf
         451  09-12-2018 12:53   conf.modules.d/01-cgi.conf
         321  09-12-2018 12:53   conf.dispatcher.d/renders/ams_publish_renders.any
         170  09-12-2018 12:53   conf.dispatcher.d/clientheaders/ams_author_clientheaders.any
         220  09-12-2018 12:53   conf.d/rewrites/xforwarded_forcessl_rewrite.rules
        1753  09-12-2018 12:53   conf.d/available_vhosts/aem_health.vhost
   ---------                     -------
       69017                     66 files
   ```
