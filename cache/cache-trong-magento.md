# Cache trong Magento

## 1. Các loại cache trong magento

### Configuration (config):&#x20;

* Magento thu thập các cấu hình từ tất cả các modules, tổng hợp nó lại và lưu kết quả vào bộ nhớ cache.&#x20;
* Nó chứa những cài đặt cụ thể được lưu trữ trong hệ thống tệp và database.&#x20;
* Sau khi sửa cấu hình, nên clean hoặc flush nó, bao gồm cả cấu hình và các cài đặt cụ thể.

### Layout (layout):

* Chứa trang layout đã biên dịch từ tất cả các components.
* Nếu thực hiện một số thay đổi với file layout, cần clean hoặc flush nó.

### Block HTML output (block\_html):&#x20;

* bao gồm các fragments trang HTML trên mỗi khối (block).&#x20;
* Nên clean hoặc flush khi có điều chỉnh các view layer.

### Collections data (collections):&#x20;

* chứa toàn bộ các câu truy vấn cơ sở dữ liệu (database query).
* Khi cần thiết, Magento sẽ tự động dọn dẹp cache, tuy nhiên Custom module có thể ghi các entry làm cho Magento không thể tự dọn chúng, lúc này chúng ta cần tự clean cache.

### DLL (db\_ddl):&#x20;

* chứa các database schema, khi cần thiết, Magento sẽ tự động dọn dẹp cache.&#x20;
* Bên thứ 3 có thể đưa bất kì dữ liệu nào vào bất kì phân đoạn (segment) nào của cache.
* Nếu thực hiện một số thay đổi với database schema, cần clean hoặc flush nó.

### Entity attribute value (eav):

* Chứa các metadata cho EAV attributes.
* Không cần phải thực hiện clean hoặc flush loại bộ nhớ này.

### Page cache (full\_page):

* Loại bộ nhớ này liên kết các trang HTML, loại bộ nhớ này cần được dọn dẹp thường xuyên, Magento tự động cleans up bộ đệm này.

### Reflection (reflection)

* Bao gồm mọi dữ liệu phản chiếu cho API interfaces.

### Translations (translate)

* Bản dịch tổng hợp từ tất cả các modules

### Integration configuration (config\_integration)

* Lưu trữ các tích hợp đã biên dịch, nên clean hoặc flush sau khi thay đổi hoặc thêm các tích hợp đã biên dịch (compiled integrations).

### Integration API configuration (config\_integration\_api)

* Chứa biên dịch cấu hình API tích hợp của Store’s Integrations.

### Web services configuration (config\_webservice)

* Là bộ nhớ đệm Web API Structure.

## 2. Tại sao chúng ta cần Magento cache?

Cache tạo ra một thư mục hệ thống, trong đó nó ghi lại tất cả các dữ liệu nhận được bởi người dùng trên internet. Khi có một request giống như vậy nữa, trang web sẽ lấy dữ liệu từ bộ nhớ cache để hiển thị chứ không cần lên server để lấy dữ liệu nữa. Với sự giúp đỡ của cache, trình duyệt không cần phải lên server lấy dữ liệu mỗi khi bạn truy cập. Nói cách đơn giản, đó là cách bộ nhớ cache management hoạt động. Do đó, các trang truy cập tải nhanh hơn đáng kể, giảm lưu lượng truy cập.&#x20;

\=> Vì vậy, chúng ta cần bộ nhớ cache để tăng tính khả dụng và làm cho trang web nhanh hơn.

Về cơ bản, có nhiều loại bộ nhớ cache, ví dụ như:

* Configuration XML files
* Cached HTML
* Session Data (technically not caching)

Nếu bạn sử dụng giá trị mặc định `file` để lưu trữ bộ nhớ cache, sau đó nó sẽ lưu trữ các giá trị này trong thư mục `var/cache` (sử dụng Zend Cache). Bạn có thể xóa tất cả các tệp này một cách an toàn, xóa hiệu quả bộ nhớ cache và Magento sẽ tái tạo chúng cho bạn.
