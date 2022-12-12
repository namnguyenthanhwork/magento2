---
cover: .gitbook/assets/magento-2-indexers.png
coverY: -21.391402714932127
layout: landing
---

# Indexer

### Definition

Indexing is how Adobe Commerce and Magento Open Source transform data such as products and categories, to improve the performance of your storefront(\*). As data changes, the transformed data must be updated or reindexed. The application has a very sophisticated architecture that stores lots of merchant data (including catalog data, prices, users, and stores) in many database tables. To optimize storefront performance, the application accumulates data into special tables using indexers

**storefront:** The online store that customers experience when they visit your Magento site.

### Indexing terminology <a href="#indexing-terminology" id="indexing-terminology"></a>

* **Dictionary:** Original data entered to the system. Dictionaries are organized in [normal form](http://en.wikipedia.org/wiki/Database\_normalization) to facilitate maintenance (updating the data).
* **Index:** Representation of the original data for optimized reading and searching. Indexes can contain results of aggregations and various calculations. Index data can be always re-created from a dictionary using a certain algorithm.
* **Indexer:** Object that creates an index.

