---
cover: .gitbook/assets/magento-2-indexers.png
coverY: -21.391402714932127
layout: landing
---

# Indexer

### Definition

Indexing is how Adobe Commerce and Magento Open Source transform data such as products and categories, to improve the performance of your **storefront(\*)**. As data changes, the transformed data must be updated or reindexed. The application has a very sophisticated architecture that stores lots of merchant data (including catalog data, prices, users, and stores) in many database tables. To optimize storefront performance, the application accumulates data into special tables using indexers

**storefront:** The online store that customers experience when they visit your Magento site.

### Indexing types

Each index can perform the following types of reindex operations:

* Full reindex, which means rebuilding all the indexing-related database tables. Full reindexing can be caused by a variety of things, including creating a new web store or new customer group. You can optionally fully reindex at any time using the [command line](manage-the-indexers.md).
* Partial reindex, which means rebuilding the database tables only for the things that changed (like changing a single product attribute or price)

The following figure shows the logic for partial reindexing.

<figure><img src=".gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

### Indexing modes <a href="#indexing-modes" id="indexing-modes"></a>

Reindexing can be performed in two modes:

* **Update on Save** - index tables are updated immediately after the dictionary data is changed.
* **Update by Schedule** - index tables are updated by cron job according to the configured schedule.

To set these options:

1. Log in to the [Admin](https://glossary.magento.com/magento-admin).
2. Click **System > Tools** **> Index Management**.
3. Select the checkbox next to each type of indexer to change.
4. From the **Actions** list, click the indexing mode.
5. Click **Submit**.

The following figure shows an example of setting indexers to Update by Schedule:

<figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

### How to reindex <a href="#how-to-reindex" id="how-to-reindex"></a>

You can reindex by:

* Using a [cron job](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs.html), which is preferred because indexing runs every minute.
* Using the [`magento indexer:reindex [indexer]`](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/manage-indexers.html#config-cli-subcommands-index-reindex) command, which reindexes selected indexers, or all indexers, one time only.

