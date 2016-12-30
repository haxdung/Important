SQL đã trở lại, lợi hại hơn bao giờ hết, áp đảo cả NoSQL ( nguồn ), doanh nghiệp hiện nay phải lựa chọn giữa SQL truyền thống hay là NoSQL, hay thậm chí NewSQL Database? Mike Stonebraker, người đã từng thắng giải Turing Award 2015, đã từng nói "one size does not fit all" (tạm dịch là một kích cỡ không thể vừa với tất cả mọi thứ được). Ý tưởng chỉ sử dụng duy nhất một database có thể phục vụ cho mọi trường hợp không còn thực tế nữa.

Nếu bạn hài lòng với hiệu suất và sức chịu của hệ quản trị cơ sở dữ liệu truyền thống SQL (như Oracle, SQL server, MySQL ) thì bạn không cần phải đọc thêm nữa. Nhưng nếu bạn đang đau đầu vì vấn đề này thì có thêm sự lựa chọn cho bạn là NoSQL và NewSQL. Nhưng chọn thằng nào?

Dưới đây là một vài lợi và hại của SQL truyền thống (tạm gọi là OldSQL), NoSQL và NewSQL, có thể giúp bạn tìm được CSDL bạn mong muốn.
OLDSQL

CSDL SQL truyền thống đã tồn tại hàng thập kỉ và có mặt gần như ở mọi app chúng ta sử dụng ngày nay. Nếu bạn triển khai app với hiệu suất tương đối thì điều đó là tuyệt vời, khỏi phải thay CSDL mới. Việc thay đổi CSDL không chỉ tốn công sức mà còn thể có nhiều rủi ro.
OLDSQL điểm mạnh

    SQL là quy chuẩn chung được chứng minh tính ổn định vài chục năm nay rồi
    Tích hợp với lớp ORM như Hibernate hoặc ActiveRecord
    Hỗ trợ tốt giao tác phía client
    Sử dụng query và report 
    Thị phần lớn trên thị trường

OLDSQL điểm yếu

    Rất khó để mở rộng (kiến trúc không hướng mở rộng). 
    SQL truyền thống được xây dựng trên ý tưởng "one size fit all", application thông thường thì sử dụng tốt nhưng sẽ gặp vấn đề khi CSDL phình to
    Điều chỉnh tham số rất phức tạp và thường yêu cầu chuyên gia để cân bằng giữa hiệu năng, an toàn dữ liệu và lượng dữ liệu sử dụng

NOSQL

Vì tiêu chí khác nhau nên cũng có rất nhiều hệ thống NoSQL khác nhau. 
Loại ưu tiên tính sẵn sàng (availability) trước

Ví dụ bạn đang nghiên cứu các dữ liệu của máy cảm biến, app của bạn ghi dữ liệu vào CSDL và thường không chỉnh sửa. Bạn muốn lưu trên cloud và không quan tâm lắm đến tính nhất quán của nó khi phân phát đến các điểm truy cập, nhiều điểm truy cập của các trung tâm dữ liệu khác ,...

Tương tác giữa app của bạn và CSDL chỉ đơn giản có "CREATE"(tạo) và "GET"(lấy). Quan trọng nhất là CSDL phải luôn chạy để nhận thêm nội dung mới và phải luôn gửi nội dung khi được yêu cầu kể cả khi nội dung đó không phải mới nhất. Các hệ thống điển hình của CSDL này là DynamoDB, Riak và Cassandra.
Loại ưu tiên tính linh hoạt(flexibility)

Loại này nổi tiếng hơn và có thể kể đến MongoDB và CouchDB, loại này lưu dữ liệu theo thiết kế JSON, thường được gọi là schemaless( không có schema ). CSDL loại này không có sự nhất quán về schema trong tất cả các bản ghi, điều này khiến việc quản lí schema ít bị đóng khung hơn nhưng cũng rối ren hơn. Những nhóm dev nhỏ và data đơn giản thì thường sử dụng loại này.

Các hệ thống khác thì mở rộng bằng việc quản lí và sắp xếp key-value tốt hơn. Redis là một thư viện nổi tiếng tạo nhiều danh sách có thể sắp xếp tiện cho xếp hạng. Tùy vào mục đích của bạn mà có thể thêm các tính năng khác cho hệ thống.
Loại ưu tiên model data khác hoặc loại đặc biệt

Phổ biến nhất là hệ thống được điều chỉnh phục vụ cho xử lý dạng đồ thị (graph) như Neo4j. Ví dụ khác là CSDL dạng array; SciDB sử dụng Python và R để truy cập MPP array data để nghiên cứu khoa học. Accumulo là sự dung hợp giữa kiểu CSDL cột rộng của Cassandra và BigTable nhưng tập trung vào từng ô hơn. Hệ thống như etcd phân phối dữ CSDL tập trng vào lưu trữ cấu hình data cho các dịch vụ khác. Elasticsearch là hệ thống nổi tiếng ứng dụng tìm kiếm text trong app.
NOSQL điểm cộng

    Thuật toán eventual-consistency đảm bảo tính sẵn sàng của CSDL
    Khả năng mở rộng tốt hơn SQL truyền thống
    Rất nhiều hệ thống NoSQL  được tối ưu để hỗ trợ data không quan hệ ví dụ như log message, XML và JSON cũng như document không có kiến trúc cụ thể nên bạn không cần quan tâm schema khi viết mà chỉ cần xem schema khi đọc.

NOSQL điểm trừ

    Hệ thống dạng này không hỗ trợ giao tác (ACID)
    OLAP query yêu cầu lượng code lớn để thực hiện. Do đó sự dễ đọc (readability) sẽ giảm khi CSDL phình to.

NEWSQL

Loại CSDL này chưa gây được tiếng vang như NoSQL. Các hệ thống NewSQL thường bắt đầu từ CSDL quan hệ và ngôn ngữ SQL query và chúng muốn giải quyết những vấn đề như khả năng mở rộng, tính bất động hoặc thiếu tính tập trung mà vẫn đảm bảo tính nhất quán.

Nhưng trong nhóm này có rất nhiều sự khác biệt. HANA được tạo chỉ để phục vụ báo cáo cho doanh nghiệp, hoàn toàn phù hợp với triển khai SAP. Hekaton thêm vào một bộ nhớ trong thông minh vào Microsoft SQL server. Cả hai hệ thống là không phân cụm (non-cluster) và được thiết kế để thay thế hoặc tăng cường việc triển khai trực tiếp OldSQL.

NuoDB là SQL database phân cụm đầu tiên tập trung vào cloud-ops: chạy trên nhiều node xuyên suốt nhiều trung tâm data và để hệ thống đằng sau quản lí dữ liệu cục bộ và nhất quán cho bạn. Giá phải trả là hiệu suất và tính nhất quán cho các công việc độc đoán (arbitrary). Công việc càng gần key-value, quản lý dữ liệu toàn hệ thống càng khó. NuoDB là hệ thống tốt nhất xét trên tính nhất quán của NewSQL.

Các loại khác tập trung vào các bản phân tích kiểu phân cụm như MemSQL. MemSQL được phân phát kèm tính năng của MySQL và thường cho phân tích OLAP nhanh hơn các OldSQL khác ( khả năng cập nhật data nhanh hơn )

VoltDB kết hợp stream bản phân tích, bảo đảm ACID và tính phân cụm. Nhờ đó, VoltDB vừa có thể là hệ thống ghi chép cho các app yêu cầu lượng data lớn, vừa có thể là bộ máy xử lý dung lượng lớn data truyền vào. VoltDB là sự lựa chọn hoàn hảo cho CSDL yêu cầu đưa ra quyết định nhanh chóng.

Nếu mục tiêu của bạn có mô hình "ingest, analyze, decide" như sau:

    Dung lượng data cần truy cập lớn
    Các sự kiện truyền vào luôn ở dạng stream (máy cảm biến, điện thoại di động, điểm truy cập mạng) và cần phải tính toán tốc độ phản hồi và phân tích mỗi một sự kiện trong thời gian thực.

NewSQL có thể là sự lựa chọn tốt với khả năng mở rộng sức chịu đựng nhưng cũng đảm bảo tính thống nhất.
NewSQL điểm hay

    Giảm độ phức tạp cho app nhờ tính nhất quán
    Tính năng SQL quen thuộc
    Phục vụ phân tích tốt hơn và khả năng mở rộng tốt hơn SQL
    Nhiều hệ thống cung cấp phân kiểu NoSQL nhưng theo kiểu data truyền thống và query model.

NewSQL điểm dở

    NewSQL thường phục vụ mục tiêu nhất định chứ không chung chung như SQL
    Kiến trúc nhớ vào bộ nhớ trong có thể không phù hợp cho các khối lượng dữ liệu quá nhiều terabytes.
