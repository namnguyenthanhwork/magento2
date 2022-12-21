---
description: Giới thiệu về elasticsearch
---

# Elasticsearch

## I. Elasticsearch là gì?

Elasticsearch là một full text search engine phát triển dựa trên nền tảng của Apache Lucene hoạt động như 1 web server phát triển trên nền tảng Java, có khả năng lưu trữ, tìm kiếm và phân tích, tổng hợp dữ liệu rất nhanh chóng (near realtime) thông qua giao thức RESTful API.&#x20;

Kể từ khi phát hành vào năm 2010 thì Elasticsearch đã nhanh chóng trở thành một trong những công cụ tìm kiếm được sử dụng thông dụng nhất và được sử dụng rộng rãi trong những trường hợp liên quan đến phân tích nhật ký và tìm kiếm văn bản, thông tin bảo mật và phân tích nghiệp vụ cũng như thông tin vận hành.

Elasticsearch có thể được sử dụng để tìm kiếm mọi loại dữ liệu, có khả năng mở rộng cực kỳ cao, tốc độ tìm kiệm theo thời gian thực, hỗ trợ multi tenancy và tìm kiếm full text.

Được các công ty, tập đoàn lớn sử dụng rộng rãi: Wikipedia, Adobe Systems, Facebook, StumbleUpon Mozilla, Quora, Github, Netflix…

## II. Ưu điểm và nhược điểm&#x20;

### 1. Ưu điểm

* Có khả năng tìm kiếm và phân tích dữ liệu.&#x20;
* Có khả năng mở rộng theo chiều ngang và tính sẵn dùng cao. Khi có một node chết thì luồng xử lý không bị ảnh hưởng và muốn mở rộng thì chỉ cần thêm node mới vào hệ thống.&#x20;
* Hỗ trợ tìm kiếm khi từ khóa tìm kiếm có thể bị sai chính tả.&#x20;
* Hỗ trợ các Elasticsearch client như Java, Javascript, PHP, Ruby...&#x20;
* Tốc độ tim kiếm rất nhanh, gần như realtime vì chỉ cần tìm kiếm 1 term là trả về các giá trị liên quan tới term đó&#x20;
* Vì được xây dựng trên Lucene nên Elasticsearch cung cấp khả năng tìm kiếm toàn văn bản (full-text) mạnh mẽ nhất.&#x20;
* Lưu trữ các thực thể phức tạp dưới dạng JSON và đánh index tất cả các field theo cách mặc định, do vậy đạt hiệu suất cao hơn.&#x20;
* Lưu trữ số lượng lớn dữ liệu dưới dạng JSON theo cách phân tán. Nó cũng cố gắng phát hiện cấu trúc của dữ liệu và đánh index của dữ liệu hiện tại, làm cho dữ liệu trở nên thân thiện với việc tìm kiếm.

### &#x20;2. Nhược điểm

* Elasticsearch được thiết kế cho mục đích search cho nên khi sử dụng thì chúng ta nên sử dụng kèm theo một DB khác như MongoDB hay Mysql.&#x20;
* Trong Elasticsearch không đảm bảo được toàn vẹn dữ liệu của các hoạt động như **Insert, Update hay Delete**. Tức khi chúng ta thực hiện thay đổi nhiều bản ghi nếu xảy ra lỗi thì sẽ làm cho logic của mình bị sai hay dẫn tới mất mát dữ liệu. Vì vậy người ta sử dụng Elasticsearch chủ yếu cho mục đích search và kết hợp với database khác chứ không sử dụng nó làm database chính.
* Không thích hợp với những hệ thống thường xuyên cập nhật dữ liệu. Sẽ rất tốn kém cho việc đánh index dữ liệu.&#x20;

## III.  Một số khái niệm cơ bản

### 1. Document

Là đơn vị nhỏ nhất để lưu trữ dữ liệu trong Elasticsearch. Đây là một đơn vị lưu trữ thông tin cơ bản trong Elasticsearch, là một JSON object đối với một số dữ liệu.

### 2. Index

Trong Elasticsearch có một cấu trúc tìm kiếm gọi là **inverted index**, nó được thiết kế để cho phép tìm kiếm full-text search. Cách thức khá đơn giản, các văn bản được tách ra thành từng từ có nghĩa sau đó sẽ được map xem thuộc văn bản nào và khi search sẽ ra kết quả cụ thể.&#x20;

Có 2 kiểu đánh index và forward index và inverted index. Bản chất của inverted index là đánh theo keyword: words -> pages còn forward đánh theo nội dung page -> words.

### 3. Shard

Shard là một đối tượng của Lucene, là tập hợp con của một Index. Một index có thể được lưu trên nhiều shard.

Một node bao gồm nhiều Shard, shard chính là đối tượng nhỏ nhât hoạt động ở mức thấp nhất, đóng vai trò lưu trữ dữ liệu

Chúng ta sẽ không bao giờ làm việc với các shard vì Elasticsearch sẽ hỗ trợ chúng ta toàn bộ việc giao tiếp cũng như tự động thay đổi các Shard khi cần thiết.&#x20;

Elasticsearch cung cấp 2 cơ chế của shard đó là primary shard và replica shard.&#x20;

* **Primary shard** sẽ lưu trữ dữ liệu và đánh Index, sau khi đánh dữ liệu xong sẽ được vận chuyển đến các replica shard, mặc định của Elasticsearch mỗi index sẽ có 5 Primary shard thì sẽ đi kèm với 1 Replica shard.&#x20;
* **Replica shard** là nơi lưu trữ dữ liệu nhân bản của Elasticsearch, đóng vai trò đảm bảo tính toàn vẹn dữ liệu khi Primary shard xảy ra vấn đề, ngoài ra nó còn giúp tăng tốc độ tìm kiếm vì chúng ta có thể cấu hình lượng Replica shard nhiều hơn cấu hình mặc định của Elasticsearch.

### 4. Node

Là trung tâm hoạt động của Elasticsearch, là nơi lưu trữ dữ liệu, tham gia thực hiện đánh index của cluster cũng như thực hiện các thao tác tìm kiếm.

Mỗi node được xác định bằng một tên riêng và không được phép trùng lặp.

### 5. Cluster

Tập hợp các nodes hoạt động cùng với nhau, chia sẻ cùng thuộc tính `cluster.name`. Chính vì thế Cluster sẽ được xác định bằng 1 `‘unique name’`. Việc định danh các cluster trùng tên sẽ gây nên lỗi cho các node vì vậy khi setup các bạn cần hết sức chú ý điểm này&#x20;

Mỗi cluster có một node chính (master), được lựa chọn một cách tự động và có thể thay thế nếu sự cố xảy ra. Một cluster có thể gồm 1 hoặc nhiều nodes. Các nodes có thể hoạt động trên cùng 1 server.&#x20;

Tuy nhiên trong thực tế, một cluster sẽ gồm nhiều nodes hoạt động trên các server khác nhau để đảm bảo nếu 1 server gặp sự cố thì server khác (node khác) có thể hoạt động đầy đủ chức năng so với khi có 2 servers. Các node có thể tìm thấy nhau để hoạt động trên cùng 1 cluster qua giao thức unicast.&#x20;

Chức năng chính của Cluster là quyết định xem shard nào được phân bổ cho node nào và khi nào thì di chuyển các Cluster để cần bằng lại Cluster.

## IV. Cấu trúc dữ liệu

Không giống như cơ sở dữ liệu quan hệ, lưu trữ dữ liệu vào hàng, ElasticSearch lưu trữ dữ liệu trong tài liệu (document).&#x20;

Tuy nhiên, ở một mức độ nào đó, 2 khái niệm này giống nhau. Với các hàng trong một bảng, bạn có các cột, với mỗi cột, mỗi hàng thì có 1 giá trị. Với tài liệu thì có key và value, cũng tương tự như vậy.&#x20;

Sự khác biệt là một tài liệu thì linh hoạt hơn một hàng, lý do chính là trong ElasticSearch tài liệu được phân nhiều cấp.&#x20;

Ví dụ: Giống như cách bạn liên kết khóa với giá trị chuỗi `“author” : “Joe”.` Một tài liệu có thể lưu mảng chuỗi `“tag” : [“cycling”, “bicycles”]`, hoặc thậm chí là cặp giá trị `“author” : {“first_name”: “Joe”, “last_name”: “Smith”}`.&#x20;

Tính linh hoạt này rất quan trọng bởi vì nó khuyến khích bạn lưu trữ những thực thế có cùng logic trong một tài liệu, trái ngược với việc lưu trữ ở các hàng và các bảng khác nhau.&#x20;

Cách dễ nhất (và có thể là nhanh nhất) là lưu trữ tất cả dữ liệu một bài viết trong cùng một tài liệu. Bằng cách này, việc tìm kiếm sẽ nhanh bởi vì bạn không cần phải liên kết với các bảng khác.&#x20;

## V. Elasticsearch lưu trữ dữ liệu như thế nào ?

Với ES, Document là đơn vị tìm kiếm và đánh index. Một index có thể bao gồm một hay nhiều Document, và một Document có thể chứa một hay nhiều Fields. Trong thuật ngữ về Database, thì một Document có thể hiểu như một table row và một Field tương ứng với một table column. ES có đặc điểm schema-free, có nghĩa là ta không cần phải chỉ rõ ra cấu trúc của schema trước khi đánh index cho các documents. Một schema sẽ bao gồm các thông tin sau:&#x20;

* Các fields
* Các ràng buộc: unique/primary key
* Các required fields&#x20;
* Đánh index và search mỗi field như thế nào Mapping là quá trình định nghĩa làm thế nào một document và các fields của nó được lưu trữ và đánh index. Mỗi index có duy nhất 1 kiểu mapping, và mapping type này sẽ quyết định cách các document sẽ được index. Mapping type gồm Meta-fields và Properties&#x20;
  * **Meta-fields:** cho phép chúng ta customize các behavior của các document&#x20;
  * **Fields/Properties:** danh sách các properties tương ứng với các document Mỗi property bao gồm 1 data-type type, là kiểu dữ liệu của prop đó. type có thể là text, keyword, date, double, boolean…

## VI. Đặc điểm và chức năng chính

ElasticSearch cho phép bạn truy cập các chức năng đánh chỉ mục và tìm kiếm dữ liệu của Lucene. Về chức năng lập chỉ mục bạn có nhiều tùy chọn về xử lý văn bản và cách lưu trữ các văn bản đã được xử lý.&#x20;

Khi tìm kiếm, bạn có nhiều câu truy vấn và bộ lọc để chọn. ElasticSearch hiển thị chức năng này thông qua RESTful API, cho phép bạn cấu hình câu truy vấn trong JSON và điều chỉnh hầu hết cấu hình, cho dù chúng cùng API.&#x20;

Ngoài những chức năng Lucene cung cấp, ElasticSearch còn bổ sung chức năng cấp cao (high level), từ bộ nhớ đệm đến phân tích thời gian thực.&#x20;

Ở mức độ trừu tượng khác là cách bạn có thể sắp xếp tài liệu: nhiều chỉ mục có thể tìm kiếm riêng hoặc cùng nhau, và bạn có thể đặt các loại tài liệu khác nhau trong mỗi chỉ mục.&#x20;

ElasticSearch đúng như tên gọi của nó co giãn (elastic). Nó được phân cụm theo mặc định – bạn có thể gọi nó là một cụm (cluster) thậm chí khi bạn chỉ có một server duy nhất – và bạn luôn luôn có thể thêm nhiều server để tăng dung lượng hoặc khả năng chịu lỗi.&#x20;

## VII. Kết luận

* Elasticsearch là một full-text search engine.&#x20;
* Elasticsearch được kế thừa từ Lucene Apache&#x20;
* Elasticsearch thực chất hoạt động như 1 web server, có khả năng tìm kiếm nhanh chóng (near realtime) thông qua giao thức RESTful API
* Elasticsearch có khả năng phân tích và thống kê dữ liệu&#x20;
* Elasticsearch chạy trên server riêng và đồng thời giao tiếp thông qua RESTful do vậy nên nó không phụ thuộc vào client viết bằng gì hay hệ thống hiện tại của bạn viết bằng gì. Nên việc tích hợp nó vào hệ thống bạn là dễ dàng, bạn chỉ cần gửi request http lên là nó trả về kết quả.&#x20;
* Elasticsearch là 1 hệ thống phân tán và có khả năng mở rộng tuyệt vời (horizontal scalability). Lắp thêm node cho nó là nó tự động auto mở rộng cho bạn.&#x20;
* Elasticsearch là 1 open source được phát triển bằng Java
* Elasticsearch là một công cụ hỗ trợ việc tìm kiếm cực kì mạnh mẽ và nhanh chóng, nhưng không phải dự án nào áp dụng Elasticsearch là hiệu quả, trái lại nó còn phát sinh ra nhiều lỗi không mong muốn. Vì vậy, hãy xem xét thật kỹ về yêu cầu của dự án trước khi áp dụng Elasticsearch
