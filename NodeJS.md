Javascript đang dần trở nên phổ biến, đi kèm với nó là rất nhiều sự thay đổi, khiến cho bộ mặt của ngành phát triển web trở nên lung linh hơn. Javascript bây giờ đã xuất hiện trên cả phía server-side, cùng với sức mạnh của nó ở phía client-side vốn dĩ đã rất mạnh mẽ, tạo nên 1 xu hướng mới, trào lưu mới trong lập trình web. Nếu so với cách đây chỉ vài năm thôi, thật khó để tưởng tượng được rằng thế giới website vẫn còn bị quanh quẩn trong những môi trường sand-box như Flash hay Java Applets.

Trước khi đi sâu vào tìm hiểu Node.js, chúng ta cần lướt qua về những thuận lợi của việc sử dụng Javascript xuyên suốt hệ thống web từ server-side đến client-side (across the stack) với khả năng hợp nhất giữa ngôn ngữ và định dạng dữ liệu (JSON). Khả năng này cho phép các nhà phát triển tái sử dụng tài nguyên 1 cách hiệu quả, cộng thêm hàng tá các tính năng mạnh mẽ khác của Javascript giúp nó, cũng như Node.js, xứng đáng có mặt trong danh sách các kỹ năng của bạn trong tương lai.

Theo Wikipedia, “Node.js là một nền tảng dựng trên trình biên dịch Google’s Chrome V8 Javascript, một nền tảng các lớp trừu tượng và một thư viện lõi, được viết chính bằng Javascript.” Theo như Ryan Dahl, cha đẻ của Node.js, “Node.js hướng đến việc tạo nên những realtime websites (websites tương tác thời gian thực). Điều này lấy cảm hứng từ Gmail. Thực vậy, với Node.js, các nhà phát triển làm việc theo event-driven (cơ thế hướng sự kiện), non-blocking (thực thi không tuần tự).

- Cuối cùng thì sau hơn 20 năm của cơ chế web resquest – response, đã xuất hiện ứng dụng realtime web, two way connection (tương tác 2 chiều).

Nói ngắn gọn về Node.js: đi đầu trong việc tạo nên những realtime websites thông qua cơ chế websocket. Cuối cùng thì sau hơn 20 năm của cơ chế web resquest – response, đã xuất hiện ứng dụng realtime web, two way connection (tương tác 2 chiều). Với Node.js, phía client và server có thể bắt đầu giao tiếp với nhau 1 cách đơn giản hơn rất nhiều (do cùng ngôn ngữ), dẫn đến dữ liệu được trao đổi 1 cách thoải mái. Với hệ thống request-response cũ, chỉ phía client là có khả năng gửi thông điệp đến server. Trước đây Flash và Java-Applets thống trị trên nền web, tuy nhiên về cơ bản chúng chỉ là các sandbox-enviroment (môi trường hộp cát), sử dụng trang web như là giao thức truyền tải dữ liệu đến đích là các client. Thêm nữa, việc chúng có cơ chế chạy độc lập và được điều khiển qua các cổng không chính thống (non-standard port) làm cho chúng ngốn nhiều tài nguyên hơn, yêu cầu hệ thống nhiều hơn.

Trong bài viết này, chúng ta sẽ thảo luận về những điểm mạnh của Node.js, cũng như lý do tại sao chúng ta sử dụng Node.js và KHÔNG sử dụng Node.js.

 
# Cơ chế làm việc

Ý tưởng chính của Node.js: sử dụng cơ chế non-blocking, event-driven I/O để làm giảm nhẹ và nâng cao hiệu quả trong việc xử lý một khối lượng rất lớn dữ liệu trên các ứng dụng realtime đa nền tảng. Tuy nhiên cần lưu ý: Node.js không phải là chiếc đũa thần nhiệm màu, có thể giúp ta vẫy tay là tạo ra được những trang web thực. Thay vào đó, Node.js là một nền tảng cho phép những nhà phát triển làm việc một cách hiệu quả với những websites realtime. Hiểu rõ điều này sẽ giúp bạn không sa lầy vào việc tôn sùng thái quá Node.js. Với những hệ thống yêu cầu cao về CPU, cần tính toán nặng nề, sử dụng Node.js là một thảm họa. Cái mà Node.js mạnh mẽ, như đã nói, là việc xây dựng được những ứng dụng network, khả năng kiểm soát được một lượng lớn các kết nối đồng thời lưu lượng cao, đồng nghĩa với việc tính tương tác rất cao.

- Node.js không phải là chiếc đũa thần nhiệm màu, có thể giúp ta vẫy tay là tạo ra được những trang web thực.

Cách mà nó chạy nền thực sự khá thú vị. Hãy so sánh với kỹ thuật web-serving truyền thống: mỗi kết nối (request) sinh ra một thread (luồng xử lý), chiếm một lượng bộ nhớ RAM hệ thống và dần dần chiếm hết dung lượng RAM khả dĩ. Node.js không như vậy. Nó chỉ chạy trên 1 thread duy nhất, sử dụng lời gọi non-blocking I/O, cho phép nó xử lý được cả ngàn kết nối cùng lúc. (Hình dưới)

Một phép tính đơn giản: giả sử mỗi thread có 2Mb bộ nhớ, chạy trên một hệ thống 8Gb RAM trên lý thuyết chỉ có thể xử lý được 4000 kết nối cùng lúc. Đấy còn chưa kể đến bộ nhớ dùng để chuyển đổi nội dung giữa các thread. Đây là viễn cảnh mà bạn sẽ phải đương đầu trong kỹ thuật web-serving truyền thống. Cùng điều kiện, Node.js vượt trội hơn hẳn với khả năng xử lý 1,000,000 kết nối cùng lúc.

Tuy nhiên việc chia sẻ chỉ một luồng đơn giữa các request của clients liệu có tối ưu? Có và không. Với những tác vụ yêu cầu tính toán nặng nề, thread đơn của Node.js sẽ bị chặn và sẽ gây ra những vấn đề ở phía client, cụ thể là những request đến sẽ phải chờ cho việc tính toán kết thúc. Bên cạnh đó, developers cũng cần cẩn thận để tránh quăng những exception vào core Node.js event-loop (vòng lặp sự kiện lõi). Việc này sẽ khiến chương trình bị ngừng, thậm chí bị crash.

Có một kỹ thuật để tránh được việc quăng lung tung exception: kiểm soát lỗi bằng cách pass nó thành tham số trong hàm callback (thay vì quăng nó ra như mấy ngôn ngữ khác). Cho dù có một số exeption khó kiểm soát có xu hướng nhảy thẳng vào mặt các devs, kha khá các công cụ và đa mô hình cho phép điều khiển tiến trình trong Node.js và biểu diễn, phục hồi các thể hiện lỗi (cho dù bạn không có khả năng phục hồi session của người dùng). Thông thường nhất là sử dụng Forever module, hay dùng một công cụ thứ 3 là Upstart and Monit.

 
# NPM: Node Package Manager (Bộ quản lý gói Node)

Khi nói về Node.js, có một điều không thể bị bỏ qua, đấy là bộ quản lý gói build-in sử dụng công cụ npm, được cài mặc định theo bộ cài Node.js. Nguyên lý của module NPM là: một bộ các thành phần mở, có khả năng tái sử dụng, có thể được cài đặt thông qua online repository (kho mã nguồn online). Danh sách các gói npm có thể được tìm thấy trên trang chủ https://npmjs.org, hoặc truy cập thông qua công cụ npm CLI, được cài tự động cùng với Node.js. Hệ sinh thái module npm mở (open source), ai cũng có thể truy cập và tải về miễn phí, cũng như tạo ra và upload module của riêng họ. Một số module npm phổ biến:

- Express: expressjs, một framework phát triển web dựa trên Sinatra, nền tảng chuẩn cho rất nhiều ứng dụng Node.js bây giờ.
- Connect: Connect là một framework server HTTP mở rộng, cung câp một bộ các plugins “hiệu năng cao” như middleware, serves, đồng thời cũng là nền tảng cho Express.
- Socket.io và sockjs: thành phần server-side của hai websocket thông dụng nhất hiện nay.
- Jade: một trong những template engine phổ biến (chuẩn viết html), dựa trên HAML, nền tảng của Expressjs.
- Mongo và mongojs: gói MongoDB cung cấp những APIs cho hệ cơ sở dữ liệu đối tượng MongoDB trong Node.js
- Redis: thư viện người dùng.
- CoffeeScript: trình biên dịch CoffeeScript cho phép những nhà phát triển viết nên chương trình Node.js bằng Coffee (uống cà phê là viết được Node.js <3)
- Underscore (lodash, lazy): thư viện cung cấp rất nhiều tiện ích, được sử dụng phổ biến nhất trong Javascript, được gói gọn trong Node.js, với cách thực thi khác biệt, hứa hẹn sẽ mang đến hiệu năng tốt hơn.
- Forever: rõ ràng đây là tiện ích thông dụng nhất, giúp cho mã Node chạy một cách liên tục.

Danh sách trên đây chỉ mang tính giới thiệu. Thực tế còn rất nhiều các module mạnh mẽ khác nữa, sẽ để giành cho bạn đọc tìm hiểu.
 
Ví dụ thực tế sử dụng Node.js

## Chat

Chat là một ứng dụng realtime, đa người dùng điển hình. Đây là ví dụ trực quan nhất về khả năng của Node.js: nhẹ, xử lý lượng lớn truy cập, dữ liệu mang tính nhạy cảm (nhưng ít tiến trình và không yêu cầu tính toán nặng), chạy đa thiết bị.

Hãy đi sâu vào cách mà một ứng dụng chat hoạt động!

Giả dụ chúng ta có một chat room trên trang web. Tại đây mọi người có thể vào và để lại tin nhắn cho một vài người hoặc tất cả trong room. Cụ thể hơn, cứ cho rằng có 3 ông đang say sưa chat chit ở trong cái room chat ấy.

Ở phía server-side, ta có một ứng dụng Express đơn giản, làm 2 công việc:

- Một bộ xử lý request GET “/” sẽ cung cấp cho trang web nội dung của khung chat và một nút “Send” để gửi tin nhắn.
- Một máy chủ websocket sẽ lắng nghe những tin nhắn mới từ websocket người dùng.

Ở phía client-side, ta có trang HTML với vài bộ xử lý, một cho nút “Send” lấy nội dung tin nhắn và gửi nó cho websocket, một cái khác lắng nghe tin nhắn đến ở websocket người dùng.

Bây giờ nếu ông A gửi tin nhắn, sẽ có những sự kiện sau xảy ra:

- Trình duyệt bắt lấy sự kiện nhấn chuột vào nút “Send”, lấy nội dung từ trường input (một đoạn text: “Alo em à? Nhớ anh không?”), đồng thời phát ra một tin nhắn websocket từ websocket người dùng đã kết nối tới server.
- Những thành phần server-side của bộ kết nối websocket nhận những tin nhắn và chuyển tiếp nó cho websocket kết nối tới ông B và ông C.
- Websocket người dùng chạy trên trang web sẽ xử lý nội dung tin nhắn và trả về cho trang web nội dung tin nhắn bằng cách thêm tin nhắn vào khung chat. Lúc này ông B và ông C sẽ thấy tin nhắn mới đến.

Vậy là đã xong ví dụ trực quan nhất cho Node.js. Đương nhiên đây chỉ là phiên bản đơn giản. Bạn hoàn toàn có thể thêm thắt những tính năng khác của riêng bạn vào (hoặc bugs :D). Sau tất cả, Node.js vẫn trung thành với luật lệ của riêng nó: phản ứng với các sự kiện, kiểm soát các kết nối đồng thời và đảm bảo tính liên tục cho trải nghiệm người dùng.

 
## API kết nối và truy xuất cơ sở dữ liệu đối tượng.

Đến giờ thì đã rõ ràng Node.js là soái ca trong việc tạo nên những ứng dụng realtime. Bên cạnh đó, việc lấy dữ liệu (JSON) từ các cơ sở dữ liệu đối tượng (MongoDB chẳng hạn) cũng không là vấn đề với Node.js. Ví dụ, nếu bạn sử dụng Rails, bạn sẽ phải convert từ JSON sang dạng nhị phân, sau đó lại phải convert ngược lại khi dữ liệu được lấy về bằng Blackbone.js hay thậm chí là bằng AJAX. Với Node.js, dữ liệu từ đầu đến cuối đều là dạng JSON. Easy. Túm lại, với Node.js, bạn sẽ chẳng cần phải quan tâm đến việc chuyển đổi kiểu dữ liệu (vì chỉ có một kiểu thoai, JSON).

 
## Luồng dữ liệu (Data Streaming)

Trên nhiều nền tảng web truyền thống, request và response HTTP được xem như những sự kiện đơn lẻ. Thực tế, chúng là các luồng. Điều này đã được nhận ra trong Node.js và được sử dụng để xây dựng nên vài tính năng hữu ích. Ví dụ, file hoàn toàn có thể được xử lý trong quá trình upload, như là mã hóa các realtime video, audio,…

# Proxy

Node.js có thể được tận dụng như là một server-side proxy, xử lý một lượng rất lớn các kết nối đồng thời theo cách thức non-blocking. Điều này đặc biệt hữu dụng khi ủy quyền cho các server khác nhau phản hồi theo thời gian, hoặc thu thập dữ liệu đa nguồn.

Ví dụ: một ứng dụng server-side giao tiếp với nguồn tài nguyên thứ 3 (third-party), lấy về dữ liệu từ nhiều nguồn khác nhau, hoặc lưu trữ tài nguyên như ảnh và video từ dịch vụ cloud.

Node.js hoàn toàn hữu ích nếu cơ sở hạ tầng proxy không tương xứng hay bạn muốn tìm kiếm giải pháp cho việc phát triển cục bộ. Khi nói thế thì ý của tôi là bạn có thể xây dựng app client-side với một server phát triển cho Node.js, đồng thời trong quá trình sản xuất bạn có thể kiểm soát tương tác với server proxy chuyên biệt (nginx, HAProxy, etc).
