---
description: Giới thiệu RabbitMQ
---

# RabbitMQ

> _Trước đây, Magento đã sử dụng bộ điều hợp MySQL để nhắn tin và các công việc định kỳ để đảm bảo việc gửi tin nhắn. Điều này không đáng tin cậy và có thể mở rộng. Để chống lại điều này, bạn có thể tích hợp RabbitMQ, bổ sung khả năng nhắn tin không đồng bộ cho Magento, đồng thời cũng có thể mở rộng và đáng tin cậy. Vậy RabbitMQ là gì?_

## I. RabbitMQ là gì?

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption><p>RabbitMQ là gì?</p></figcaption></figure>

Với hàng chục nghìn người dùng, RabbitMQ là một trong những nhà môi giới tin nhắn mã nguồn mở phổ biến nhất. Từ [T-Mobile](https://www.youtube.com/watch?v=1qcTu2QUtrU) đến [Runtastic](https://medium.com/@runtastic/messagebus-handling-dead-letters-in-rabbitmq-using-a-dead-letter-exchange-f070699b952b), RabbitMQ được sử dụng trên toàn thế giới tại các công ty khởi nghiệp nhỏ và doanh nghiệp lớn.

RabbitMQ rất nhẹ và dễ triển khai tại cơ sở và trên đám mây. Nó hỗ trợ nhiều giao thức nhắn tin. RabbitMQ có thể được triển khai trong các cấu hình phân tán và liên kết để đáp ứng các yêu cầu về tính sẵn sàng cao, quy mô lớn.

RabbitMQ chạy trên nhiều hệ điều hành và môi trường đám mây, đồng thời cung cấp [nhiều loại công cụ dành cho nhà phát triển cho hầu hết các ngôn ngữ phổ biến](https://www.rabbitmq.com/devtools.html)&#x20;

{% hint style="info" %}
Một tin nhắn có thể bao gồm bất kỳ loại thông tin nào.&#x20;

Ví dụ: nó có thể có thông tin về một quy trình hoặc tác vụ sẽ bắt đầu trên một ứng dụng khác (thậm chí có thể ở trên một máy chủ khác) hoặc nó có thể chỉ là một tin nhắn văn bản đơn giản. Phần mềm quản lý hàng đợi lưu trữ các tin nhắn cho đến khi ứng dụng nhận kết nối và lấy tin nhắn ra khỏi hàng đợi. Sau đó, ứng dụng nhận sẽ xử lý thông báo.
{% endhint %}

{% hint style="info" %}
Trình môi giới tin nhắn hoạt động như một người trung gian cho các dịch vụ khác nhau

Ví dụ: ứng dụng web, như trong ví dụ này). Chúng có thể được sử dụng để giảm tải và thời gian phân phối của máy chủ ứng dụng web bằng cách ủy thác các tác vụ thường chiếm nhiều thời gian hoặc tài nguyên cho bên thứ ba không có công việc nào khác.
{% endhint %}

Tuy nhiên khả năng định tuyến thông điệp linh hoạt mới là điều làm cho RabbitMQ thực sự nổi bật trong vô số các công nghệ truyền thông điệp hiện nay.

## II. Lợi ích của RabbitMQ

Có một số lợi ích khi sử dụng RabbitMQ, chẳng hạn như:

* Nhắn tin không đồng bộ
* Phân cụm
* Liên bang
* Hàng đợi có sẵn cao
* Đa giao thức
* Giao diện người dùng quản lý
* Hệ thống plugin

Có một số nhiệm vụ/hoạt động thực hiện trong cấu trúc của trang web thương mại khi khách hàng đặt hàng từ trang web, chẳng hạn như:

* Tạo đơn hàng
* Nhận thanh toán
* Quản lý chứng khoán
* Cho phép liên lạc qua email và văn bản
* Gửi/Nhận dữ liệu đơn hàng lên hệ thống SAP/CRM/ERP
* Gửi dữ liệu đến phân tích

Khi tất cả các hoạt động này được thực hiện trong thời gian thực, sẽ có thêm thời gian để hoàn tất quy trình đặt hàng, điều này có thể ảnh hưởng tiêu cực đến doanh nghiệp. RabbitMQ có thể giúp chuyển hầu hết các tác vụ này thành hàng đợi và xử lý chúng sau đó thông qua nhắn tin không đồng bộ, do đó cho phép máy chủ web phản hồi nhanh chóng.

## III. Tính năng của RabbitMQ

Một số tính năng chính chính của RabbitMQ bao gồm:

* **Độ tin cậy:** Các đặc điểm chính của RabbitMQ có ảnh hưởng ngay lập tức đến hiệu suất bao gồm tính bền bỉ, phản hồi gửi, xác nhận của nhà xuất bản và tính sẵn sàng cao.
* **Phân cụm tích hợp:** Việc phân cụm trong RabbitMQ được tạo ra với hai mục tiêu. Nó vẫn cho phép người tiêu dùng và nhà sản xuất tiếp tục hoạt động trong trường hợp một nút bị lỗi, mở rộng thông lượng nhắn tin một cách tuyến tính bằng cách thêm các nút mới.
* **Bảo mật:** Nó được cung cấp bởi RabbitMQ ở các cấp độ khác nhau. Có thể đạt được các kết nối máy khách an toàn bằng cách yêu cầu Kiểm tra chứng chỉ ứng dụng khách và giao tiếp chỉ có SSL. Máy chủ ảo có thể có các điều khiển truy cập của người dùng để đảm bảo cách ly thông báo cấp cao.
* **Định tuyến linh hoạt:** Để định tuyến, RabbitMQ đi kèm với một số loại trao đổi tích hợp. Tin nhắn thường được định tuyến thông qua các trao đổi trước khi chúng đến hàng đợi trong định tuyến thông thường. Người dùng cũng có thể liên kết các trao đổi với nhau để định tuyến phức tạp hoặc thậm chí phát triển loại trao đổi của họ dưới dạng plugin.

### 1. Hàng đợi tin nhắn là gì ?

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption><p>Hàng đợi tin nhắn là gì ?</p></figcaption></figure>

**Hàng đợi tin nhắn (message queueing)** giúp các ứng dụng phần mềm khác nhau không có tích hợp sẵn có thể kết nối và trao đổi thông tin. Hàng đợi tin nhắn được tạo thành từ nhà sản xuất, nhà môi giới (phần mềm hàng đợi tin nhắn) và người tiêu dùng. Nhà sản xuất là ứng dụng khách tạo thông báo được gửi đến nhà môi giới. Nhà môi giới lưu trữ các tin nhắn và đợi người tiêu dùng kết nối với nó và lấy tin nhắn.

<figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption><p><strong>Hàng đợi tin nhắn (message queueing)</strong></p></figcaption></figure>

**Queue** còn được gọi là **message broker** là hàng đợi các tin nhắn được đặt giữa hai phần của hệ thống để chúng liên lạc với nhau tin nhắn là dữ liệu được truyền giữa người gửi và người nhận và ví dụ về tin nhắn có thể là một phần của hệ thống yêu cầu một phần khác của hệ thống bắt đầu xử lý một tác vụ, tác vụ này có thể là yêu cầu mở rộng quy mô hình ảnh hoặc nhật ký sẽ được lưu trữ, một thông báo cũng có thể chứa thông tin về một tác vụ đã hoàn thành như khi nào đơn đặt hàng được xử lý hoặc nó có thể chỉ là một thông điệp đơn giản với thông tin.

{% hint style="warning" %}
**Tại sao phải sử dụng hàng đợi tin nhắn?**

**Tại sao phải sử dụng hàng đợi Messeage queueing?**
{% endhint %}

**Ưu điểm**

* Tách kiến trúc Service

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

* Không đồng bộ

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

* Giải quyết số lượng truy vấn cao hơn hệ thống

<figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

**Nhược điểm:**

* Tăng độ phức tạp của hệ thống.
* Miss tin nhắn.
* Tính nhất quán của hệ thống.

### **2. Exchanges và Queue**

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption><p><strong>Exchanges và Queue</strong></p></figcaption></figure>

**Tổng quan:**

* Các Publisher gửi thông điệp đến các Exchange
* Các Exchange định tuyến cácthông điệp đến hàng đợi và các Exchange khác
* RabbitMQ gửi `ack` đến các Publisher ứng với mỗi thông điệp nhận được
* Các Consumer duy trì kết nối TCP liên tục với RabbitMQ và khai báo (các) hàng đợi mà chúng tiêu thụ
* RabbitMQ push thông điệp đến các Consumer
* Các Consumer gửi `ack` khi tiêu thụ thành công hoặc thất bại
* Các thông điệp được xóa khỏi hàng đợi khi đã tiêu thụ thành công

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

Nhiều Publisher, nhiều Consumer độc lập. Các Publisher gửi thông điệp của chúng đến cùng một Exchange, Exchange này định tuyến mỗi thông điệp đến ba queue, mỗi queue trong số đó có một Consumer duy nhất.

RabbitMQ cũng cho phép các Consumer khác nhau cùng tiêu thụ một queue.

Nhiều Publisher, một queue với nhiều Consumer cạnh tranh nhau. Đây là những Consumer cạnh tranh, chúng cạnh tranh để tiêu thụ các thông điệp của một hàng đợi duy nhất. Chúng ta thường sẽ mong đợi rằng trung bình mỗi Consumer sẽ tiêu thụ một phần ba số thông điệp của hàng đợi này.

Chúng ta có thể sử dụng những Consumer cạnh tranh để mở rộng quy trình xử lý thông điệp, và với RabbitMQ việc này rất đơn giản, chỉ cần thêm hoặc xóa Consumer theo yêu cầu nghiệp vụ bài toán. Cho dù bạn có bao nhiêu Consumer cạnh tranh nhau đi nữa, thì RabbitMQ cũng sẽ đảm bảo rằng các thông điệp được gửi đến chỉ một Consumer duy nhất.

#### Exchange:

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

* **Direct Exchange** hướng tin nhắn đến một hàng đợi cụ thể bằng cách xem Khóa định tuyến. Khóa định tuyến trong tin nhắn được so sánh bằng với các khóa gốc trên các ràng buộc
* Topic Exchange định tuyến tin nhắn đến một hoặc nhiều hàng đợi bằng cách xem Khóa định tuyến. Khóa định tuyến trong tin nhắn được so sánh để khớp với các mẫu Khóa định tuyến trên các liên kết. Trao đổi chủ đề hỗ trợ “Khớp khóa định tuyến nghiêm ngặt” giống như Trao đổi trực tiếp nhưng sẽ cũng thực hiện khớp ký tự đại diện bằng cách sử dụng dấu sao (\*) và hàm băm (#) làm phần giữ chỗ.
* Fanout Exchange sao chép và định tuyến một tin nhắn đã nhận tới tất cả các hàng đợi được liên kết với nó bất kể Khóa định tuyến. Khóa định tuyến được cung cấp đơn giản là bị bỏ qua.

### 3. Khi nào nên sử dụng RabitMQ?&#x20;

1. Người dùng chương trình của bạn gửi một số tệp nhất định cần được chuyển mã sang một số định dạng khác, chẳng hạn như video hoặc âm thanh. Nếu bạn không thiết lập quy trình nền hoặc hàng đợi, người dùng sẽ phải đợi quy trình kết thúc trước khi chuyển sang bước tiếp theo. Đây có thể là một khoảng thời gian rất dài trong trường hợp video.
2. Bạn có thể sử dụng RabbitMQ để kết nối các ứng dụng tiêu dùng với các ứng dụng cũ bằng cách sử dụng các phần bổ trợ hiện có (hoặc thiết kế phần bổ trợ của riêng bạn). Ví dụ, các thư viện máy khách JMS và trình cắm Dịch vụ Thông báo Java có sẵn để kết nối với các ứng dụng JMS.
3. RabbitMQ là một lựa chọn tuyệt vời nếu bạn cần một trình trung chuyển tin nhắn linh hoạt và đáng tin cậy. Cộng đồng RabbitMQ đang hoạt động và mở rộng, đồng thời có rất nhiều tài liệu và hỗ trợ. Khi bạn không yêu cầu khả năng phát lại tin nhắn về một chủ đề, RabbitMQ có thể hữu ích. Mặc dù RabbitMQ không thể phát lại các sự kiện, nhưng các thông báo đã truyền vẫn được giữ nguyên; do đó, bạn có thể sử dụng nhà sản xuất để phát lại tin nhắn.
4. Khi một hành động nhất định xảy ra trong ứng dụng của bạn, bạn có thể muốn thông báo cho người dùng. Bạn chỉ có thể cung cấp các giá trị cho người dùng bằng cách tách mã liên quan đến việc gửi thông báo (qua email, SMS, v.v.). RabbitMQ (và các hàng đợi tin nhắn phức tạp khác) cũng có thể được sử dụng để cung cấp các quy tắc hệ thống rất phức tạp để quản lý luồng tin nhắn, chẳng hạn như số lượng hàng đợi, người tiêu dùng và các ràng buộc được tạo.
5. Khi các tin nhắn phải được định tuyến trên một số ứng dụng dành cho người tiêu dùng, RabbitMQ có thể là lựa chọn tốt nhất. Trao đổi hàm băm liên tục của nó có thể được sử dụng để trải rộng quá trình xử lý tải trên một dịch vụ giám sát phân tán.
6. Người dùng có thể tải các tệp lên nền tảng Softonic, nơi chúng sẽ được quét vi-rút và thông tin về tệp được thu thập trước khi phổ biến cho những người dùng khác. Khi quá trình tải lên hoàn tất, người dùng sẽ nhận được thông báo. Điều này có thể đạt được vì tính năng Kiến trúc microservice của RabbitMQ cho phép các máy chủ web trả lời các truy vấn nhanh chóng.

### 4. Các trường hợp sử dụng RabbitMQ

Định tuyến phức tạp – nếu bạn muốn định tuyến tin nhắn giữa nhiều ứng dụng tiêu thụ như trong kiến ​​trúc vi dịch vụ, RabbitMQ có thể là lựa chọn tốt nhất của bạn. Trao đổi hàm băm nhất quán của RabbitMQ có thể cân bằng quá trình xử lý tải trên một dịch vụ giám sát phân tán. Bạn cũng có thể sử dụng các trao đổi thay thế để định tuyến phần sự kiện cụ thể đến các dịch vụ cụ thể cho thử nghiệm A/B.&#x20;

Ứng dụng cũ – một trường hợp sử dụng khác của RabbitMQ là triển khai nó bằng cách sử dụng các plugin có sẵn (hoặc xây dựng plugin của riêng bạn) để kết nối các ứng dụng tiêu dùng với các ứng dụng cũ. Ví dụ: giao tiếp với các ứng dụng JMS bằng cách sử dụng trình cắm Java Message Service (JMS) và thư viện máy khách JMS.&#x20;

## IV. So sánh giữa Kafka và RabbitMQ

{% hint style="info" %}
**Đâu là sự khác biệt giữa Message Broker và Hệ thống nhắn tin Xuất bản/Đăng ký (Pub/Sub)?**
{% endhint %}

Message Broker là các mô-đun phần mềm cho phép các ứng dụng, dịch vụ và hệ thống giao tiếp và trao đổi thông tin. Các nhà môi giới tin nhắn thực hiện điều này bằng cách dịch các tin nhắn giữa các giao thức nhắn tin chính thức, cho phép các dịch vụ phụ thuộc lẫn nhau trực tiếp “nói chuyện” với nhau, ngay cả khi chúng được viết bằng các ngôn ngữ khác nhau hoặc chạy trên các nền tảng khác.

Message Broker xác thực, định tuyến, lưu trữ và gửi tin nhắn đến người nhận được chỉ định. Các nhà môi giới hoạt động với vai trò trung gian giữa các ứng dụng khác, cho phép người gửi gửi tin nhắn mà không cần biết vị trí của người tiêu dùng, cho dù họ có hoạt động hay không hoặc thậm chí có bao nhiêu người trong số họ tồn tại.

Tuy nhiên, Publish/ Subscribe là mẫu phân phối thông báo cho phép nhà sản xuất xuất bản từng thông báo họ muốn.

| Kafka vs RabbitMQ | RabbitMQ                                            | Kafka                              |
| ----------------- | --------------------------------------------------- | ---------------------------------- |
| Performance       | 4k-10k messages per second                          | 1 million messages per second      |
| Message Retention | Acknowledgment based                                | Policy-based( e.g 30days)          |
| Data Type         | Transactional                                       | Operational                        |
| Consumer Mode     | <p>Smart broker/dumb consumer</p><p> </p>           | Dumb broker/smart consumer         |
| Topology          | Exchange type: Direct, Fan out, Topic, header-based | Publish/subscribe based            |
| Payload Size      | No constraints                                      | Default 1MB limit                  |
| Usage Cases       | Simple use cases                                    | Massive data/high throughput cases |

#### Pull and Push Approach

Cơ chế đẩy của RabbitMQ ngăn người tiêu dùng biết về bất kỳ truy xuất tin nhắn nào. Nhà môi giới đảm bảo khách hàng nhận được tin nhắn.

Ngoài ra, nó trả về một xác nhận sau khi xử lý dữ liệu để đảm bảo thông điệp đến được với khách hàng. Khi có phản hồi tiêu cực, tin nhắn sẽ được gửi một lần nữa bằng cách thêm vào hàng đợi.

Kafka cung cấp cơ chế kéo cho phép khách hàng yêu cầu dữ liệu theo lô từ nhà môi giới. Thông minh, người tiêu dùng giữ một tab ở phần bù của lần gặp tin nhắn gần đây nhất. Bằng cách sử dụng offset, nó sắp xếp dữ liệu theo thứ tự của các phân vùng.
