# Cache

## I. Giới thiệu cache

### 1. Cache là gì ?

* Cache là phần cứng hoặc phần mềm được tích hợp sẵn với tác dụng lưu trữ dữ liệu tạm thời.
* Cache sẽ lưu lại data để những lần request kế tiếp cần data đó sẽ được trả về nhanh hơn.
* Data lưu trong cache có thể là kết quả của lần tính toán trước hoặc một phần dữ liệu được lưu ở nơi khác.

<figure><img src="https://lh3.googleusercontent.com/5hRm_jB33XsVoplTrdw7XZmHkbI3G-yZFHhIOO3hBAPmSF1g9mnDCtlDCdDe-szErzBzQODD23pqH2NOQdzmX4Lh4TbPrC0Zwn61A4i6g5wW9wNB1cDGzmkiIdVOX2jQRmut49bWsp1TqCxbzN3S3ZXq5U1XLWFsNutOVEoC_2YANFuLhAdcdVTeJUZA3A" alt=""><figcaption><p>Cache là gì ?</p></figcaption></figure>

Vd: Khi người dùng truy cập một trang web mới, trình duyệt của họ cần tải xuống dữ liệu để load và hiển thị nội dung trên trang (HTML, css, js, png, jpg…). Để tăng tốc quá trình này cho lần truy cập sau này của người dùng, các trình duyệt sẽ lưu các dữ liệu đó vào cache. Do đó, lần sau khi người dùng truy cập trang web đó, thay vì lên tới server thì nó sẽ chỉ vào cache để lấy dữ liệu trả về cho người dùng.

### 2. Cache hit và cache miss

* Cache hit là khi dữ liệu yêu cầu được tìm thấy trong cache. Đầu tiên, bộ xử lý trung tâm (CPU) tìm kiếm dữ liệu ở vị trí bộ nhớ gần nhất, thường là primary cache (bộ nhớ đệm chính). Nếu dữ liệu yêu cầu được tìm thấy trong bộ nhớ cache, nó được gọi là cache hit.
* Cache miss là khi dữ liệu yêu cầu không được tìm thấy trong cache hoặc có được lưu trong bộ nhớ cache nhưng đã hết hạn và nội dung không được cập nhật khi so sánh với cùng một nội dung trên máy chủ gốc. Đối với mỗi yêu cầu mới, bộ xử lý sẽ ưu tiên tìm kiếm dữ liệu đó trong primary cache trước tiên. Nếu dữ liệu không được tìm thấy tại đây, nó được coi là một cache miss. Cache miss gây ra sự chậm trễ vì nội dung được yêu cầu không có sẵn trong primary cache, do đó, request phải được chuyển tiếp đến các cache  ở cấp khác để thực hiện truy vấn. Trong trường hợp xấu nhất, request của người dùng sẽ phải gửi đến tận máy chủ lưu trữ gốc để lấy dữ liệu.

### 3. Các kỹ thuật trong cache

#### 3.1. Read through

<figure><img src="https://lh5.googleusercontent.com/TGT_6Oqo_wERT1SAG_fLZmP-cRpL7bCR-3EbwD6WNA5itBf3smZztXTsOSNqSYLy86zYuICs_-O0OYNzzYL32WH4J4gmPIpdLC8l3fBawTwghKzCcXrhme6oYd33w0Bubk1VnlBxWLIsWY0OmVQfDG1huag2JJSEQTvww3DOyhOrbUf5asxwOMGfgZnN_A" alt=""><figcaption><p>Read through</p></figcaption></figure>

* Tìm dữ liệu trong cache, nếu tìm thấy => trả dữ liệu về
* Nếu không tìm thấy trong cache, đọc từ “database” => ghi data vào cache => trả data về
* Ưu điểm:
  * Không load toàn bộ data lên cache
  * Trong trường hợp cache nhiều node, khi một node bị sự cố, hệ thống vẫn không bị hư hại.
* Nhược điểm:
  * Trong trường hợp cache miss, delay cao do cần đến 3 network round trip.
  * Nếu có thay đổi trong database và cache chưa expire => trả về data cũ cho ứng dụng.

#### 3.2. Read aside

<figure><img src="https://lh6.googleusercontent.com/jyaouJtyMgjsX0fFaitKcwafqZW3bXshrMRJ7wcXYuNCP1Qw2cpu5xlmhO1OF8ps8J8WQwYcBEw717ozrKkMDlavPiU03khjQFyCtV-jxZSvs9x610a6Pv_utpHQbd6JF2RDWzlRz3mlb42dA5mzQD-CdCGFYvDzleB5ZYcSLxiT3i4TW6GaUY5l6_HJHg" alt=""><figcaption><p>Read aside</p></figcaption></figure>

Cache aside có vấn đề về security, vd khi dữ liệu yêu cầu không được tìm thấy trong cache, và trong database cũng không có data, nếu hacker spam request đó, thì lúc này app sẽ liên tục thực hiện đi thực hiện lại request không có dữ liệu trả về này, liên tục đọc và trả database, lúc này sẽ làm overload database.&#x20;

\


1. #### Write around:&#x20;

Write-around Cache có khả năng ghi lại các hoạt động trực tiếp vào bộ nhớ, hoàn toàn bỏ qua Cache.&#x20;

![](https://lh5.googleusercontent.com/wR5bzN5htNPtCo9eG87xvId5l4LqL42zes2DsHSU7xRZ6wk7IoGT7PKN3wK1JYb9CohuGcEP-GU9v288TrzzGsdUTGY4Jo6wuz8S\_u43DC2IoBsNaxQVJRNyIiu4ZanCJszl0WwwF9z9j2gfxwkNNnX\_v3WqgH5RUr0REdoNVnUO7OcDjBdE6hvtqPtEVA)

\


1. #### Write back:

![](https://lh6.googleusercontent.com/DQN71l0QUU7u41f7ARM6KWz0EHYY3xrbndZHqe9k2xOhk8c4pccqV3pugh8Anlu5J4fFVGphJ\_pAVoTiB\_WxOTQX7HOa91oPBGNdxF6p8qpf38TpURTt3GzARiGthw6IRTMDQjRqLUbgXWFXGCdTQYZuoPC5deX9NCF7n69nvxLYTyChi\_bXYcpfDl00rg)

Write back lưu rất nhiều vào cache, lâu lâu mới update vào database 1 lần.

\


1. #### Write through:

![](https://lh6.googleusercontent.com/Tkdvxb6Qn3452-w628u3Urx1mfWubJ3K9sS763Ei9I-LOGD2Lz2W0VZHZzXZmZr-ba5EijB3RpihC8k-k4\_ai-uQ-KzcFZRXT8d56gbzjdUeMi4gHa-RCy8GXpGR3RyehUN1QhInlToeYEucJPNkYncnZLyaFLSnlu4vTmX4VzzasRqlBByugp\_AvjB4sg)

* Thêm/cập nhật database cũng sẽ cập nhật trong cache.
* Hai tác vụ này nên xảy ra trong cùng một transaction.
* Ưu điểm:
*
  * Đảm bảo dữ liệu trong cache luôn là mới nhất.
  * Thích hợp cho những hệ thống cần nhu cầu đọc lớn và không chấp nhận dữ liệu bị cũ.
* Nhược điểm:
*
  * Mỗi thao tác write sẽ gồm 2 thao tác: write database và write cache.
  * Để đảm bảo tính đồng bộ, nếu write cache hay database thất bại => thao tác write thất bại.
  * Phần lớn data trong cache không được đọc đến. Giải quyết bằng cách thêm expire.

\


1. #### Write behind caching

Data được ghi trực tiếp vào cache, sau đó data mới được ghi vào database bất đồng bộ.

* Ưu điểm:
*
  * Write/read trên cache => tăng performance.
  * Tách biệt ứng dụng khỏi “database failure”.
* Nhược điểm:
*
  * Bất đồng bộ giữa cache và database.
  * Write cache và database không được xử lý trong một transaction nên phải có cơ chế rollback nếu dữ liệu không thể write vào database.

1. ## Cache trong Magento
2.
   1. Các loại cache trong magento

* Configuration (config):&#x20;
* Magento thu thập các cấu hình từ tất cả các modules, tổng hợp nó lại và lưu kết quả vào bộ nhớ cache.&#x20;
* Nó chứa những cài đặt cụ thể được lưu trữ trong hệ thống tệp và database.&#x20;
* Sau khi sửa cấu hình, nên clean hoặc flush nó, bao gồm cả cấu hình và các cài đặt cụ thể.
* Layout (layout):
* Chứa trang layout đã biên dịch từ tất cả các components.
* Nếu thực hiện một số thay đổi với file layout, cần clean hoặc flush nó.
* Block HTML output (block\_html):&#x20;
* bao gồm các fragments trang HTML trên mỗi khối (block).&#x20;
* Nên clean hoặc flush khi có điều chỉnh các view layer.
* Collections data (collections):&#x20;
* chứa toàn bộ các câu truy vấn cơ sở dữ liệu (database query).
* Khi cần thiết, Magento sẽ tự động dọn dẹp cache, tuy nhiên Custom module có thể ghi các entry làm cho Magento không thể tự dọn chúng, lúc này chúng ta cần tự clean cache.
* DLL (db\_ddl):&#x20;
* chứa các database schema, khi cần thiết, Magento sẽ tự động dọn dẹp cache.&#x20;
* Bên thứ 3 có thể đưa bất kì dữ liệu nào vào bất kì phân đoạn (segment) nào của cache.
* Nếu thực hiện một số thay đổi với database schema, cần clean hoặc flush nó.
* Entity attribute value (eav):
* Chứa các metadata cho EAV attributes.
* Không cần phải thực hiện clean hoặc flush loại bộ nhớ này.
* Page cache (full\_page):
* Loại bộ nhớ này liên kết các trang HTML, loại bộ nhớ này cần được dọn dẹp thường xuyên, Magento tự động cleans up bộ đệm này.
* Reflection (reflection): bao gồm mọi dữ liệu phản chiếu cho API interfaces.
* Translations (translate): bản dịch tổng hợp từ tất cả các modules
* Integration configuration (config\_integration): lưu trữ các tích hợp đã biên dịch, nên clean hoặc flush sau khi thay đổi hoặc thêm các tích hợp đã biên dịch (compiled integrations).
* Integration API configuration (config\_integration\_api): chứa biên dịch cấu hình API tích hợp của Store’s Integrations.
* Web services configuration (config\_webservice): là bộ nhớ đệm Web API Structure.

\


1. ### Tại sao chúng ta cần Magento cache?

Cache tạo ra một thư mục hệ thống, trong đó nó ghi lại tất cả các dữ liệu nhận được bởi người dùng trên internet. Khi có một request giống như vậy nữa, trang web sẽ lấy dữ liệu từ bộ nhớ cache để hiển thị chứ không cần lên server để lấy dữ liệu nữa. Với sự giúp đỡ của cache, trình duyệt không cần phải lên server lấy dữ liệu mỗi khi bạn truy cập. Nói cách đơn giản, đó là cách bộ nhớ cache management hoạt động. Do đó, các trang truy cập tải nhanh hơn đáng kể, giảm lưu lượng truy cập.&#x20;

\=> Vì vậy, chúng ta cần bộ nhớ cache để tăng tính khả dụng và làm cho trang web nhanh hơn.

\


* Về cơ bản, có nhiều loại bộ nhớ cache, ví dụ như:
*
  * Configuration XML files
  * Cached HTML
  * Session Data (technically not caching)

Nếu bạn sử dụng giá trị mặc định 'file' để lưu trữ bộ nhớ cache, sau đó nó sẽ lưu trữ các giá trị này trong thư mục var/cache (sử dụng Zend Cache). Bạn có thể xóa tất cả các tệp này một cách an toàn, xóa hiệu quả bộ nhớ cache và Magento sẽ tái tạo chúng cho bạn.

1. ### Một số command với cache trong Magento
2.
   1. #### View the status of the cache

|   bin/magento cache:status |
| -------------------------- |

1. #### Enable cache

enable cache nào sẽ tự động clean cache đó.

| <p>  bin/magento cache:enable [type]...[type]</p><p>   EX:</p><p>   bin/magento cache:enable db_ddl full_page</p> |
| ----------------------------------------------------------------------------------------------------------------- |

\


Để enable toàn bộ cache, bỏ qua \[type]:

|    bin/magento cache:enable |
| --------------------------- |

\


1. #### Disable cache

| <p>   bin/magento cache:disable [type]...[type]</p><p>   EX:</p><p>   bin/magento cache:disable db_ddl full_page   </p> |
| ----------------------------------------------------------------------------------------------------------------------- |

\


Để disable toàn bộ cache, bỏ qua \[type]:

|    bin/magento cache:disable |
| ---------------------------- |

\


1. #### Clean and flush cache

|   bin/magento cache:clean \[type]...\[type] |
| ------------------------------------------- |

\


|   bin/magento cache:flush \[type]...\[type] |
| ------------------------------------------- |

\


Nếu không nhập \[type] thì sẽ xóa tất cả các loại cache:

|   bin/magento cache:flush |
| ------------------------- |

\


1. ### Kỹ thuật cache trong Magento

![](https://lh4.googleusercontent.com/q4DsCaF2-WDzg2EqFBcTEtdPeXBlvaW\_YHp793T4pFool24jUzDfL6spNuv2U6fN1Y59q1HDgs4\_IJEHzjzR8ZffWNIUEyhCGTjxezzR2iMQMfhPh0Kc9mCif7aY8sFZn3tG0\_Ba4\_BFPAtRJkM0YXvhzUxB7Ka\_YmCJGvFZ7E7dX\_tIEnYB0lyUWZYI1g)

* Giải thích mô hình:&#x20;
* Khi chúng ta edit hoặc insert => Magento tự động xóa Cache
* Những client đến sau không tìm thấy data trong cache (cache miss) => xuống Mysql đọc data => save vào cache.
* Nhược điểm: Khi số lượng request cùng 1 lúc trên 2k, mà không tìm thấy data trong cache => Dẫn đến MYSQL bị sập (MySQL chỉ chịu đc 2k request/1s)
* Cách khắc phục: đó là nguyên nhân ra đời của RabbitMQ, RabbitMQ để đồng bộ lưu cache và lập hàng chờ.

\


1. ### Thao tác command line trong redis

|   docker compose exec -it redis bash |
| ------------------------------------ |

\


| <p>  redis-cli ping</p><p>   // output: pong</p> |
| ------------------------------------------------ |

\


| <p>  redis-cli monitor</p><p>   // OR</p><p>   redis-cli keys *</p><p><br></p><p>   //after run this command line, refresh page</p><p>   //output: list Key + Value of cache</p> |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

\


\=> ctrl + C to  cancel

| <p>  docker compose exec -it redis bash</p><p>   redis-cli</p><p>   hget “&#x3C;key name>” “d”</p> |
| -------------------------------------------------------------------------------------------------- |

\


1. ### Tạo một cache type

Tạo một file cache type mới theo đường dẫn: \<module\_dir>/etc/cache.xml và thêm code vào file cache.xml vừa tạo

| <p>&#x3C;?xml version="1.0"?></p><p>&#x3C;config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:Cache/etc/cache.xsd"></p><p>    &#x3C;type name="%cache_type_id%" translate="label,description" instance="VendorName\ModuleName\Model\Cache\Type\CacheType"></p><p>        &#x3C;label>CMS CACHE Type Label&#x3C;/label></p><p>        &#x3C;description>Cache Type Description&#x3C;/description></p><p>    &#x3C;/type></p><p>&#x3C;/config></p> |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

\


![](https://lh3.googleusercontent.com/eDlAfnPqEMkRAloKGnU1loaiAQhe4dawYHwfHxokPYu9zv35b58smcgyrWmpJw06Jz87s4R\_HS\_6-hgPw\_2DqEbSgiNSlY6m1BV8vG2QlKHrOl6ntKzpZGY\_eifXXFw4FOIGBgzd6Hne2h0NeNT\_QB1lZfYae2xNATkApQLOo-AuOZeJORGFpx98wIBzoQ)

\


Tạo thư mục php theo đường dẫn như attribute instance&#x20;

\


| <p>&#x3C;?php</p><p>/**</p><p> * Copyright © Magento, Inc. All rights reserved.</p><p> * See COPYING.txt for license details.</p><p> */</p><p><br></p><p>namespace VendorName\ModuleName\Model\Cache\Type\CacheType;</p><p><br></p><p>use Magento\Framework\App\Cache\Type\FrontendPool;</p><p>use Magento\Framework\Cache\Frontend\Decorator\TagScope;</p><p><br></p><p>/**</p><p> * System / Cache Management / Cache type "Your Cache Type Label"</p><p> */</p><p>class CacheType extends TagScope</p><p>{</p><p>    /**</p><p>     * Cache type code unique among all cache types</p><p>     */</p><p>    const TYPE_IDENTIFIER = '%cache_type_id%';</p><p><br></p><p>    /**</p><p>     * The tag name that limits the cache cleaning scope within a particular tag</p><p>     */</p><p>    const CACHE_TAG = '%CACHE_TYPE_TAG%';</p><p><br></p><p>    /**</p><p>     * @param FrontendPool $cacheFrontendPool</p><p>     */</p><p>    public function __construct(FrontendPool $cacheFrontendPool)</p><p>    {</p><p>        parent::__construct(</p><p>            $cacheFrontendPool->get(self::TYPE_IDENTIFIER),</p><p>            self::CACHE_TAG</p><p>        );</p><p>    }</p><p>}</p><p><br></p> |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

\










