# Command với cache trong Magento

## 1. View the status of the cache

```
bin/magento cache:status
```

## 2. Enable cache

enable cache nào sẽ tự động clean cache đó.

```
bin/magento cache:enable [type]...[type]
```

Ex:

```
bin/magento cache:enable db_ddl full_page
```

Để enable toàn bộ cache, bỏ qua `[type]`:

```
bin/magento cache:enable
```

## 3. Disable cache

```
bin/magento cache:disable [type]...[type]
```

Ex:

```
bin/magento cache:disable db_ddl full_page

```

Để disable toàn bộ cache, bỏ qua `[type]`

```
bin/magento cache:disable
```

## 4. Clean and flush cache

```
bin/magento cache:clean [type]...[type]
```

```
bin/magento cache:flush [type]...[type]
```

Nếu không nhập `[type]` thì sẽ xóa tất cả các loại cache:

```
bin/magento cache:flush
```
