FireBase có thể rất mạnh mẽ đối với ứng dụng backend, nó bao gồm việc lưu trữ dữ liệu, xác thực người dùng, static hosting......Nên lập trình viên chỉ cần chú tâm đến việc nâng cao trải nghiệm người dùng.

# Firebase Realtime Database

Dữ liệu trong cơ sở dữ liệu Firebase của bạn được lưu trữ dưới dạng JSON và đồng bộ realtime đến mọi kết nối client. Khi bạn xây dựng những ứng dụng đa nền tảng như Android, IOS và JavaScrip SDKs, tất cả các client của bạn sẽ chia sẻ trên một cơ sở dữ liệu Firebase và tự động cập nhật với dữ liệu mới nhất.

## Tự động tính toán quy mô ứng dụng của bạn

Khi ứng dụng của bạn muốn phát triển, bạn không cần lo lắng về việc nâng cấp máy chủ...Firebase sẽ xử lý việc tự động cho bạn. Các máy chủ của Firebase quản lý hàng triệu kết nối đồng thời và hàng tỉ lượt truy vấn mỗi tháng.

## Các tính năng bảo mật lớp đầu

Tất cả dữ liệu được truyền qua một kết nối an toàn SSL với một chứng nhận 2048-bit. Cở sở dữ liệu truy vấn và việc xác nhận  được điều khiển tại một cấp độ chi tiết sử dụng theo một số các quy tắc mềm dẻo security rules language.  Tất cả các logic bảo mật dữ liệu của bạn được tập trung ở một chỗ để dễ dàng cho việc cập nhật và kiểm thử.

## Làm việc offline

Ứng dụng Firebase của bạn sẽ duy trì tương tác bất chấp một số các vấn đề về internet xảy ra. Trước khi bất kỳ dữ liệu được ghi đến server thì tất  cả dữ liệu lập tức sẽ được viết vào một cơ sử dữ liệu Firebase ở local. Ngay khi có thể kết nối lại, client đó sẽ nhận bất kỳ thay đổi mà nó thiếu và đồng bộ hoá nó với trạng thái hiện tại server.

# Xác thực người dùng

Với Firebase, bạn có thể dễ dàng xác thực người dùng từ ứng dụng của bạn trên Android, iOS và JavaScript SDKs chỉ với một vài đoạn mã. Firebase đã xây dựng chức năng cho việc xác thực người dùng với Email, Facebook, Twitter, GitHub, Google, và xác thực nạc danh. Các ứng dụng sử dụng chức năng xác thực của FireBase có thể giải quyết được vấn đề khi người dùng đăng nhập, nó sẽ tiết kiện thời gian và rất nhiều các vấn đề phức tạp về phần backend. Hơn nữa bạn có thể tích họp xác thực người dùng với các chức năng backend đã có sẵn sử dụng  custom auth tokens.

# Firebase Hosting

Phát triển ứng dụng web của bạn trong thời gian ngắn với các hosting tĩnh đã được cung cấp sẵn. Tất cả các kết nối được phân phối qua SSL từ CDN trên toàn thể giới của Firebase

- Triểu khai siêu tốc:Việc triển khai sử dụng các công cụ dòng lệnh Firebase  và có thể quay trở lại với phiên bản trước chỉ với một cú click chuột. Tất cả các ứng dụng sẽ có đường dẫn mặc đinh ở sau firebaseapp.com (https://techmastervn.firebaseio.com/) và nếu trả phí thì có thể triểu khai một tên miền tuỳ chỉnh.

- SSL bởi default:Mọi ứng dụng được xử lý thông qua một kết nối an toàn, và Firebase đã cẩn thận cung cấp SSL cert cho bạn. 
