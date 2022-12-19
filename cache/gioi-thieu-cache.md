# Giới thiệu cache

## 1. Cache là gì ?

* Cache là phần cứng hoặc phần mềm được tích hợp sẵn với tác dụng lưu trữ dữ liệu tạm thời.
* Cache sẽ lưu lại data để những lần request kế tiếp cần data đó sẽ được trả về nhanh hơn.
* Data lưu trong cache có thể là kết quả của lần tính toán trước hoặc một phần dữ liệu được lưu ở nơi khác.

<figure><img src="https://lh3.googleusercontent.com/5hRm_jB33XsVoplTrdw7XZmHkbI3G-yZFHhIOO3hBAPmSF1g9mnDCtlDCdDe-szErzBzQODD23pqH2NOQdzmX4Lh4TbPrC0Zwn61A4i6g5wW9wNB1cDGzmkiIdVOX2jQRmut49bWsp1TqCxbzN3S3ZXq5U1XLWFsNutOVEoC_2YANFuLhAdcdVTeJUZA3A" alt=""><figcaption><p>Cache là gì ?</p></figcaption></figure>

Vd: Khi người dùng truy cập một trang web mới, trình duyệt của họ cần tải xuống dữ liệu để load và hiển thị nội dung trên trang (HTML, css, js, png, jpg…). Để tăng tốc quá trình này cho lần truy cập sau này của người dùng, các trình duyệt sẽ lưu các dữ liệu đó vào cache. Do đó, lần sau khi người dùng truy cập trang web đó, thay vì lên tới server thì nó sẽ chỉ vào cache để lấy dữ liệu trả về cho người dùng.

## 2. Cache hit và cache miss

* Cache hit là khi dữ liệu yêu cầu được tìm thấy trong cache. Đầu tiên, bộ xử lý trung tâm (CPU) tìm kiếm dữ liệu ở vị trí bộ nhớ gần nhất, thường là primary cache (bộ nhớ đệm chính). Nếu dữ liệu yêu cầu được tìm thấy trong bộ nhớ cache, nó được gọi là cache hit.
* Cache miss là khi dữ liệu yêu cầu không được tìm thấy trong cache hoặc có được lưu trong bộ nhớ cache nhưng đã hết hạn và nội dung không được cập nhật khi so sánh với cùng một nội dung trên máy chủ gốc. Đối với mỗi yêu cầu mới, bộ xử lý sẽ ưu tiên tìm kiếm dữ liệu đó trong primary cache trước tiên. Nếu dữ liệu không được tìm thấy tại đây, nó được coi là một cache miss. Cache miss gây ra sự chậm trễ vì nội dung được yêu cầu không có sẵn trong primary cache, do đó, request phải được chuyển tiếp đến các cache  ở cấp khác để thực hiện truy vấn. Trong trường hợp xấu nhất, request của người dùng sẽ phải gửi đến tận máy chủ lưu trữ gốc để lấy dữ liệu.

## 3. Các kỹ thuật trong cache

### 3.1. Read through

<figure><img src="https://lh5.googleusercontent.com/TGT_6Oqo_wERT1SAG_fLZmP-cRpL7bCR-3EbwD6WNA5itBf3smZztXTsOSNqSYLy86zYuICs_-O0OYNzzYL32WH4J4gmPIpdLC8l3fBawTwghKzCcXrhme6oYd33w0Bubk1VnlBxWLIsWY0OmVQfDG1huag2JJSEQTvww3DOyhOrbUf5asxwOMGfgZnN_A" alt=""><figcaption><p>Read through</p></figcaption></figure>

* Tìm dữ liệu trong cache, nếu tìm thấy => trả dữ liệu về
* Nếu không tìm thấy trong cache, đọc từ “database” => ghi data vào cache => trả data về

**Ưu điểm:**

* Không load toàn bộ data lên cache
* Trong trường hợp cache nhiều node, khi một node bị sự cố, hệ thống vẫn không bị hư hại.

**Nhược điểm:**

* Trong trường hợp cache miss, delay cao do cần đến 3 network round trip.
* Nếu có thay đổi trong database và cache chưa expire => trả về data cũ cho ứng dụng.

### 3.2. Read aside

<figure><img src="https://lh6.googleusercontent.com/jyaouJtyMgjsX0fFaitKcwafqZW3bXshrMRJ7wcXYuNCP1Qw2cpu5xlmhO1OF8ps8J8WQwYcBEw717ozrKkMDlavPiU03khjQFyCtV-jxZSvs9x610a6Pv_utpHQbd6JF2RDWzlRz3mlb42dA5mzQD-CdCGFYvDzleB5ZYcSLxiT3i4TW6GaUY5l6_HJHg" alt=""><figcaption><p>Read aside</p></figcaption></figure>

Cache aside có vấn đề về security, vd khi dữ liệu yêu cầu không được tìm thấy trong cache, và trong database cũng không có data, nếu hacker spam request đó, thì lúc này app sẽ liên tục thực hiện đi thực hiện lại request không có dữ liệu trả về này, liên tục đọc và trả database, lúc này sẽ làm overload database.&#x20;

### 3.3. Write around

Write-around Cache có khả năng ghi lại các hoạt động trực tiếp vào bộ nhớ, hoàn toàn bỏ qua Cache.&#x20;

<figure><img src="https://lh5.googleusercontent.com/wR5bzN5htNPtCo9eG87xvId5l4LqL42zes2DsHSU7xRZ6wk7IoGT7PKN3wK1JYb9CohuGcEP-GU9v288TrzzGsdUTGY4Jo6wuz8S_u43DC2IoBsNaxQVJRNyIiu4ZanCJszl0WwwF9z9j2gfxwkNNnX_v3WqgH5RUr0REdoNVnUO7OcDjBdE6hvtqPtEVA" alt=""><figcaption><p>Write around</p></figcaption></figure>

### 3.4. Write back

<figure><img src="https://lh6.googleusercontent.com/DQN71l0QUU7u41f7ARM6KWz0EHYY3xrbndZHqe9k2xOhk8c4pccqV3pugh8Anlu5J4fFVGphJ_pAVoTiB_WxOTQX7HOa91oPBGNdxF6p8qpf38TpURTt3GzARiGthw6IRTMDQjRqLUbgXWFXGCdTQYZuoPC5deX9NCF7n69nvxLYTyChi_bXYcpfDl00rg" alt=""><figcaption><p>Write back</p></figcaption></figure>

Write back lưu rất nhiều vào cache, lâu lâu mới update vào database 1 lần.

### 3.4. Write through

<figure><img src="https://lh6.googleusercontent.com/Tkdvxb6Qn3452-w628u3Urx1mfWubJ3K9sS763Ei9I-LOGD2Lz2W0VZHZzXZmZr-ba5EijB3RpihC8k-k4_ai-uQ-KzcFZRXT8d56gbzjdUeMi4gHa-RCy8GXpGR3RyehUN1QhInlToeYEucJPNkYncnZLyaFLSnlu4vTmX4VzzasRqlBByugp_AvjB4sg" alt=""><figcaption></figcaption></figure>

* Thêm/cập nhật database cũng sẽ cập nhật trong cache.
* Hai tác vụ này nên xảy ra trong cùng một transaction.

**Ưu điểm:**

* Đảm bảo dữ liệu trong cache luôn là mới nhất.
* Thích hợp cho những hệ thống cần nhu cầu đọc lớn và không chấp nhận dữ liệu bị cũ.

**Nhược điểm:**

* Mỗi thao tác write sẽ gồm 2 thao tác: write database và write cache.
* Để đảm bảo tính đồng bộ, nếu write cache hay database thất bại => thao tác write thất bại.
* Phần lớn data trong cache không được đọc đến. Giải quyết bằng cách thêm expire.

### 3.5. Write behind caching

Data được ghi trực tiếp vào cache, sau đó data mới được ghi vào database bất đồng bộ.

**Ưu điểm:**

* Write/read trên cache => tăng performance.
* Tách biệt ứng dụng khỏi “database failure”.

**Nhược điểm:**

* Bất đồng bộ giữa cache và database.
* Write cache và database không được xử lý trong một transaction nên phải có cơ chế rollback nếu dữ liệu không thể write vào database.ng clean cache đó.
