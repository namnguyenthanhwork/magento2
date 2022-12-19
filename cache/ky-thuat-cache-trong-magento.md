# Kỹ thuật cache trong Magento

## 1. Kỹ thuật cache trong Magento

<figure><img src="https://lh4.googleusercontent.com/q4DsCaF2-WDzg2EqFBcTEtdPeXBlvaW_YHp793T4pFool24jUzDfL6spNuv2U6fN1Y59q1HDgs4_IJEHzjzR8ZffWNIUEyhCGTjxezzR2iMQMfhPh0Kc9mCif7aY8sFZn3tG0_Ba4_BFPAtRJkM0YXvhzUxB7Ka_YmCJGvFZ7E7dX_tIEnYB0lyUWZYI1g" alt=""><figcaption><p>Kỹ thuật cache trong Magento</p></figcaption></figure>

Giải thích mô hình:&#x20;

* Khi chúng ta edit hoặc insert => Magento tự động xóa Cache
* Những client đến sau không tìm thấy data trong cache (cache miss) => xuống Mysql đọc data => save vào cache.

Nhược điểm: Khi số lượng request cùng 1 lúc trên 2k, mà không tìm thấy data trong cache => Dẫn đến MYSQL bị sập (MySQL chỉ chịu đc 2k request/1s)

Cách khắc phục: đó là nguyên nhân ra đời của RabbitMQ, RabbitMQ để đồng bộ lưu cache và lập hàng chờ.

## 2. Thao tác command line trong redis

```
docker compose exec -it redis bash
```

```
redis-cli ping  // output: pong
```

```
redis-cli monitor
  // OR
redis-cli keys *

//after run this command line, refresh page
//output: list Key + Value of cache
```

\=> ctrl + C to  cancel

```
docker compose exec -it redis bash
redis-cli
hget “<key name>” “d”
```

## 3. Tạo một cache type

Tạo một file cache type mới theo đường dẫn: \<module\_dir>/etc/cache.xml và thêm code vào file cache.xml vừa tạo

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:Cache/etc/cache.xsd">
    <type name="%cache_type_id%" translate="label,description" instance="VendorName\ModuleName\Model\Cache\Type\CacheType">
        <label>CMS CACHE Type Label</label>
        <description>Cache Type Description</description>
    </type>
</config>

```

Tạo thư mục php theo đường dẫn như attribute instance&#x20;

```php
<?php
/**
 * Copyright © Magento, Inc. All rights reserved.
 * See COPYING.txt for license details.
 */


namespace VendorName\ModuleName\Model\Cache\Type\CacheType;


use Magento\Framework\App\Cache\Type\FrontendPool;
use Magento\Framework\Cache\Frontend\Decorator\TagScope;


/**
 * System / Cache Management / Cache type "Your Cache Type Label"
 */
class CacheType extends TagScope
{
    /**
     * Cache type code unique among all cache types
     */
    const TYPE_IDENTIFIER = '%cache_type_id%';


    /**
     * The tag name that limits the cache cleaning scope within a particular tag
     */
    const CACHE_TAG = '%CACHE_TYPE_TAG%';


    /**
     * @param FrontendPool $cacheFrontendPool
     */
    public function __construct(FrontendPool $cacheFrontendPool)
    {
        parent::__construct(
            $cacheFrontendPool->get(self::TYPE_IDENTIFIER),
            self::CACHE_TAG
        );
    }
}

```
