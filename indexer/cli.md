---
description: Command line index in magento2
cover: ../.gitbook/assets/bg2.png
coverY: 64.47963800904976
---

# CLI

### View a list of all indexers

```bash
bin/magento indexer:info
```

The list displays as follows:

```
design_config_grid                       Design Config Grid
customer_grid                            Customer Grid
catalog_category_product                 Category Products
catalog_product_category                 Product Categories
catalogrule_rule                         Catalog Rule Product
catalog_product_attribute                Product EAV
inventory                                Inventory
catalogrule_product                      Catalog Product Rule
cataloginventory_stock                   Stock
targetrule_product_rule                  Product/Target Rule
targetrule_rule_product                  Target Rule/Product
catalog_product_price                    Product Price
catalogsearch_fulltext                   Catalog Search
salesrule_rule                           Sales Rule
```

### View indexer status <a href="#view-indexer-status" id="view-indexer-status"></a>

Use this command to view the status of all indexers or specific indexers. For example, find out if an indexer needs to be reindexed.

Command options:

```bash
bin/magento indexer:status [indexer]
```

Where `[indexer]` is a space-separated list of indexers. Omit `[indexer]` to view the status of all indexers.

Sample result:

```
+----------------------+------------------+-----------+---------------------+---------------------+
| Title                | Status           | Update On | Schedule Status     | Schedule Updated    |
+----------------------+------------------+-----------+---------------------+---------------------+
| Catalog Product Rule | Reindex required | Save      |                     |                     |
| Catalog Rule Product | Reindex required | Save      |                     |                     |
| Catalog Search       | Ready            | Save      |                     |                     |
| Category Products    | Reindex required | Schedule  | idle (0 in backlog) | 2021-06-28 09:45:53 |
| Customer Grid        | Ready            | Schedule  | idle (0 in backlog) | 2021-06-28 09:45:52 |
| Design Config Grid   | Ready            | Schedule  | idle (0 in backlog) | 2018-06-28 09:45:52 |
| Inventory            | Ready            | Save      |                     |                     |
| Product Categories   | Reindex required | Schedule  | idle (0 in backlog) | 2021-06-28 09:45:53 |
| Product EAV          | Reindex required | Save      |                     |                     |
| Product Price        | Reindex required | Save      |                     |                     |
| Stock                | Reindex required | Save      |                     |                     |
+----------------------+------------------+-----------+---------------------+---------------------+
```

### Reindex <a href="#reindex" id="reindex"></a>

Use this command to reindex all or selected indexers one time only.

This command reindexes one time only. To keep indexers up to date, you must set up a [cron job](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs.html?lang=en).

Command options:

```bash
bin/magento indexer:reindex [indexer]
```

Where `[indexer]` is a space-separated list of indexers. Omit `[indexer]` to reindex all indexers.

Sample result:

```
Design Config Grid index has been rebuilt successfully in <time>
Customer Grid index has been rebuilt successfully in <time>
Category Products index has been rebuilt successfully in <time>
Product Categories index has been rebuilt successfully in <time>
Catalog Rule Product index has been rebuilt successfully in <time>
Product EAV index has been rebuilt successfully in <time>
Inventory index has been rebuilt successfully in <time>
Catalog Product Rule index has been rebuilt successfully in <time>
Stock index has been rebuilt successfully in <time>
Product Price index has been rebuilt successfully in <time>
Catalog Search index has been rebuilt successfully in <time>
```

{% hint style="info" %}
Reindexing all indexers can take a long time for stores with large numbers of products, customers, categories, and promotional rules.
{% endhint %}

### Reset indexer <a href="#reset-indexer" id="reset-indexer"></a>

Use this command to invalidate the status of all indexers or specific indexers.

Command options:

```bash
bin/magento indexer:reset [indexer]
```

Where `[indexer]` is a space-separated list of indexers. Omit `[indexer]` to invalidate all indexers.

Sample result:

```
Design Config Grid indexer has been invalidated.
Customer Grid indexer has been invalidated.
Category Products indexer has been invalidated.
Product Categories indexer has been invalidated.
Catalog Rule Product indexer has been invalidated.
Product EAV indexer has been invalidated.
Inventory indexer has been invalidated.
Catalog Product Rule indexer has been invalidated.
Stock indexer has been invalidated.
Product Price indexer has been invalidated.
Catalog Search indexer has been invalidated.
```

### Configure indexers <a href="#configure-indexers" id="configure-indexers"></a>

Use this command to set the following indexer options:

* **Update on save (`realtime`)**: Indexed data is updated when a change is made in the Admin. (For example, the category products index is reindex after products are added to a category in the Admin.) This is the default.
* **Update by schedule (`schedule`)**: Data is indexed according to the schedule set by your cron job.

#### Display the current configuration <a href="#display-the-current-configuration" id="display-the-current-configuration"></a>

To view the current indexer configuration:

```bash
bin/magento indexer:show-mode [indexer]
```

Where `[indexer]` is a space-separated list of indexers. Omit `[indexer]` to show all indexers’ modes. For example, to show the mode of all indexers:

Sample result:

```
Design Config Grid:                                Update on Save
Customer Grid:                                     Update on Save
Category Products:                                 Update on Save
Product Categories:                                Update on Save
Catalog Rule Product:                              Update on Save
Product EAV:                                       Update on Save
Inventory:                                         Update on Save
Catalog Product Rule:                              Update on Save
Stock:                                             Update on Save
Product Price:                                     Update on Save
Catalog Search:                                    Update on Save
```

Before switching indexer modes, we recommend putting your website to [maintenance](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/maintenance-mode.html?lang=en) mode and [disable cron jobs](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/app/properties/crons-property.html?lang=en#disable-cron-jobs). This ensures you do not suffer database locks.

To specify the indexer configuration:

```bash
bin/magento indexer:set-mode {realtime|schedule} [indexer]
```

Where:

* `realtime`—Sets the selected indexers to update on save.
* `schedule`—Sets the specified indexers to save according to the cron schedule.
* `indexer`—Is a space-separated list of indexers. Omit `indexer` to configure all indexers the same way.

For example, to change only the category products and product categories indexers to update on schedule, enter:

```bash
bin/magento indexer:set-mode schedule catalog_category_product catalog_product_category
```

Sample result:

```
Index mode for Indexer Category Products was changed from 'Update on Save' to 'Update by Schedule'
Index mode for Indexer Product Categories was changed from 'Update on Save' to 'Update by Schedule'
```

The indexers-related database triggers are added when the indexer mode is set to `schedule` and removed when the indexer mode is set to `realtime`. If the triggers are missing from your database while the indexers are set to `schedule`, change the indexers to `realtime` and then change them back to `schedule`. This resets the triggers.
