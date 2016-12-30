Trong tất cả các loại tấn công nhằm vào các trang web hiện này thì SQL Injection là một trong những loại tấn công nguy hiểm và phổ biến nhất, nó đã gây thiệt hại không nhỏ cho các doanh nghiệp và tổ chức trong nhiều năm trở lại đây. Trước khi tìm cách bảo về website của chúng ta trước nó thì cần phải tìm hiểu xem liệu nó là gì và cách nó hoạt động ra sao.

Tóm lại, SQL injection -  còn gọi tắt là SQLi - sử dụng những lỗ hổng trong các input đầu vào của trang web để nhằm mục đích gây hại cho trang web của chúng ta. Cụ thể là chúng dựa vào các câu lệnh SQL để đánh cắp thông tin nhạy cảm của người dùng, thay đổi cơ sở dữ liệu, cản trở sự hoạt động của hệ thống... trong trường hợp xấu nhất có thể xảy ra thì nó có thể chiềm quyền sử dụng cơ sở dữ liệu của chúng ta . (RIP me).

Dưới đây là những gì mà mình nghĩ là bạn nên biết về SQL injection và làm sao để bảo vệ trang web của bạn chống lại nó. (Hi vọng với những thông tin mình cung cấp có thể "make your website better" ).
SQL Injection tấn công như nào?

    Biết người biết ta - trăm trận trăm thắng -  Tôn tử

SQL injection (gọi là SQLi cho ngắn vậy) được tổ chức (organized) bằng cách gửi các lệnh SQL độc hại đến các máy chủ cơ sở dữ liệu thông qua các request mà trang web bạn cho phép, ví dụ như các lệnh đăng nhập. Bất kì các đầu vào trang web của bạn ( các thẻ input, các query string, cookies và files ) để có thể được sử dụng để gửi các mã độc.

Để xem các mà nó làm việc, bạn có thể nhìn vào form đăng nhập dưới đây. Nó bao gồm hai input để nhập username và password, một nút submit để gửi dữ liệu.

Khi người dùng nhập thông tin đăng nhập và bấm login, thông tin của người dùng sẽ được gửi một tới servert thông qua một POST request sau đó sẽ được gán vào một câu lệnh SQL. Đoạn code đó sẽ trông như này:
```sql
$sql_command = "select * from users where username = '" . $_POST['username']; $sql_command .= "' AND password = '" . $_POST['password'] . "'"; 
```
Đoạn code này sẽ sau đó sẽ được lên máy chủ cơ sở dữ liệu. kết quả trả về của nó sẽ kiểm tra được người dùng nhập vào có hợp lệ hay có phải là người dùng trong hệ thống hay không?. Một ví dụ là người dùng có username là "john" và password là "123456" (đừng bao giờ dùng mật khẩu này) thì đoạn mã trên sẽ chuyển thành đoạn SQL như sau:
```sql
SELECT * FROM users WHERE username='john' AND password='123456' 
```
Đấy là trường hợp người dùng nhập thông tin hợp lệ (ở đây có nghĩa là họ nhập chính xác username chỉ bao gồm chữ hoặc số ...) Vậy thì điều gì xảy ra khi học nhập thông tin như bên dưới:

Kết quả của đoạn code phía bên trên bây giờ sẽ được biên dịch thành như này:
```sql
SELECT * FROM users WHERE username='john' OR 1=1; 
-- ' AND password='123456' 
```
Phần kiểm tra password đã bị comment lại. Kết quả trả về sẽ là thông tin của người dùng có username là 'john' mà không cần thiết phải biết mật khẩu.

Bằng thủ thuật này thì ta đã có quyền quy cập của người dùng mà chỉ cần biết username của người đó.

Đây là một trong những ví dụ điển hình và đơn giản nhất của SQLi. Bằng một vài thủ thuật thì người dùng có thể thêm, sửa thậm chí là xóa các người dùng trong hệ thống. học có thể đánh cắp toàn bộ thông tin người dùng chỉ bằng một đoạn lệnh rất ngắn.

Trong trường hợp xấu hơn, khi mà kết nối đến máy chủ cơ sở dữ liệu được tạo ra (và kiểm soát) bởi một tài khoản admin (giống như tài khoản root trong MySQL ), kẻ tấn công có thể làm nhiều điều hơn thế. Hắn có thể sử dụng lỗ hổng SQLi để tạo tài khoản người dùng trên máy chủ bị tấn công, kích hoạt tính năng Remote Desktop, thiết lập SMB chia sẽ các thư mục và tải lên các mã độc khác.
Vậy làm thế nào để bảo vệ khỏi tấn công SQL Injection?

Với mỗi một kênh đầu vào ( input element, file, cookies ...) sẽ tương ứng với một kiểu tấn công SQLi. Cách tốt nhất để bảo vệ khỏi tấn công SQLi là kiểm soát các dữ liệu đầu vào trang web của bạn. 

Dưới đây sẽ là một vài phương pháp hữu ích để đảm bảo rằng input người dùng nhập vào là an toàn:

**Nguyên tắc 1: Đừng bao giờ tin vào thông tin người dùng nhập vào.**

Nguyên tắc đầu tiên cũng là lớn nhất về input người dùng nhập và là "don't trust and verify" -  nó có nghĩa là tất cả các form từ người dùng nhập lên cần phải được kiểm duyệt một cách nghiêm chỉnh. Nó không chỉ bao gồm những input boxes như kiểu textarea hay input text mà nó còn bao gồm rất nhiều các khác ví dụ như hidden input, query string parameters, cookies và file uploads.

Không phải là browser của chúng ta không cho phép thay đổi các thông tin mà ta gửi đi thì ta không thể thay đổi nó. Có một tool tên là Burp Suite cho phép người dùng có thể capture lại HTTP request và thay đổi nó, thêm các hidden input trước khi gửi nó đến server. Và nếu bạn nghĩ rằng mình thông minh bằng cách sử dụng Base64 để mã hóa dữ liệu của mình thì nó có thể giải mã một cách dễ dàng, sửa đổi và tái mã hóa.

**Nguyên tắc 2 : Validate dữ liệu trên server side.**

Validation là quá trình để đảm bảo dữ liệu người dùng gửi lên là hợp lệ. Ví dụ ở trong PHP, bạn có thể dùng hàm mysql_real_escape_string() để loại bỏ những kí tự có thể gây ảnh hưởng đến câu lệnh SQL.

Đoạn code đầu tiên sẽ sửa thành như này: 
```sql
$con=mysqli_connect("localhost","user","password","db");
$username = mysqli_real_escape_string($con, $_POST['username']); 
$password = mysqli_real_escape_string($con, $_POST['password']); 
$sql_command = "select * from users where username = '" . $username; $sql_command .= "' AND password = '" . $password . "'"; 
```
Edit một chút đã giúp bảo vệ code của chúng ta trước tấn công SQLi bằng cách thêm vào kí tự (\) trước các dấu nháy đơn mà người dùng có ý thêm vào.

Một số lưu ý về tính toán:  Nếu bạn đã thêm việc validate dữ liệu ở client side thì người dùng có thể pass qua những validation phía client side bằng các sửa các mã HTML họ nhận được hay tắt các javascript ở phía client đi. 

Trong một số ngôn ngữ lập trình, chẳng hạn như ASP.NET, bao gồm các tính năng tự động xem xét các dữ liệu đầu vào và sử dụng các bộ lọc để loại bỏ nó. Nhưng điều này vẫn có thể bị tin tặc lách qua nếu đủ tinh tế. Dù sao thì việc kiểm tra dữ liệu đầu vào cũng chẳng bao giờ là điều quá thận trọng cả.

**Nguyên tắc 3: Sử dụng command parameters**

Một lựa chọn tốt hơn để chông tấn công SQLi là sử dụng placeholder để giữ chỗ trong câu lệnh SQL sau này khi người dùng nhập dữ liệu thì sẽ điền đầy vào đó.

Ví dụ về đoạn code sau: 
```sql
SqlCommand cmd = new SqlCommand ("SELECT * FROM users WHERE username=@username AND password=@password",con); 

SqlParameter username = new SqlParameter(); username.ParameterName = "@username"; username.value = txtUsername.Text; cmd.Parameters.Add(username); 

SqlParameter password = new SqlParameter(); password.ParameterName = "@password"; password.value = txtPassword.Text; cmd.Parameters.Add(password); 
```
Đầu tiên ta sẽ tạo ra một SqlCommand  object và sử dụng placeholder  @parameter_name trong đoạn lệnh, nó sẽ được thêm vào khi người dùng thêm điền dữ liệu vào.

Sau đó tạo thêm một instances của  SqlParameter objects, sau đó nội dụng người dùng nhập vào sẽ được lưu vào đây thay vì chèn trực tiếp vào câu lệnh SQL.

Cuối cùng, ta thêm cái  SqlParameter object vào SqlCommand object's Parameter collection, và dữ liệu người dùng nhập vào sẽ được truyền vào trong câu lệnh SQL.

Trong PHP sẽ có PDO và mysqli có thể giải quyết giống như ASP.net. Bạn có thể tham khảo ở đây.

**Nguyên tắc 4: Định nghĩa kiểu dữ liệu cho input**

Tips này giành cho những ngôn ngữ như kiểu PHP vậy, khi bạn gõ code thì không thường xuyên xác định kiểu dữ liệu cho các biến

Việc định nghĩa rõ ràng kiểu dữ liệu cho dữ liệu đầu vào như một cách để loại bỏ những dữ liệu có thể gây sai cho câu lệnh SQL.

Ví dụ như: 
```
$age = (int)$_POST['age']; 
```
Cách làm trên chỉ đúng để xác thực với kiểu của dữ liệu chứ nó không thể kiểm soát việc nhập tuổi có đúng không ví dụ như > 1000 tuổi hay giá trị âm chẳng hạn.

Và một trong những cách tốt để chống tấn công SQLi là tránh sử dụng dấu nhanh đơn trong lệnh SQL khi không có string được truyền vào. Bạn sử dụng đoạn code này: 
```sql
$sql_command = "select * from users where age = " . $age; 
```
sẽ an toàn hơn việc sử dụng dòng lệnh này:
```sql
$sql_command = "select * from users where age = '" . $age . "'"; 
```

**Làm thế nào để nhổ tận gốc lỗ hổng SQL Injection.**

Bạn nên kiểm tra code của mỗi trang, đặc biệt là những nơi bạn kết hơp giữa nội dung (contents), các lệnh, các chuỗi ... với dữ liệu từ phía người dùng. Rà soát lại toàn bộ mã nguồn, tìm kiếm các lỗ hổng bảo mật là một phần vốn có của quá trình phát triền phần mềm của bạn.

Bạn cũng có thể sử dụng một tools để "quét" như sqlmap để tìm kiếm các lỗ hổng mà SQLi có thể lợi dụng trong trang web của bạn. Trong một vài trường hợp, thì hacker cũng dùng nó để tìm ra lỗ hổng để tấn công trang web của bạn.
Vài dòng cuối cùng

Không quan tâm bạn đã đổ bao nhiêu tiền cho việc xây dựng hệ thống bảo mật cho website của bạn thì bạn vẫn phải chuẩn bị cho việc một ngày nào đó SQLi sẽ ghé thăm nhà bạn và "làm khó dễ" đôi chút cái hệ thống đó. Cẩn thận chưa bao giờ là đủ và chúng ta cần hiểu rằng đừng bao giờ cho hacker  chiến thắng dù chỉ một lần.

Dưới đây còn một vài tips mà có thể giúp bạn hạn chế tối đa ảnh hưởng từ việc trở thành nạn nhận của SQLi
Tránh quyền quản trị 

Sử dụng tài khoản "root" để kết nối ứng dụng web của bạn tới máy chủ database là một trong những sai sót tệ nhất mà bạn cần tránh. Những tác hại của nó thì mình đã trình bày ở trên. Việc để hacker chiếm quyền quản lý thì việc dữ liệu còn nguyên vẹn là hoàn toàn khó có thể xảy ra.

**Mã hóa những dữ liệu nhạy cảm.**

Hãy mà hóa những dữ liệu nhạy cảm trong cơ sở dữ liệu của bạn. Nó bao gồm mật khẩu, câu hỏi và câu trả lời bí mật, các dữ liệu về tài chính, thông tin sức khỏe và những thông tin có ích cho hacker. Nó đảm bảo rằng nếu mà thông tin mà có lộ ra ngoài thì tin tặc cũng không thể sử dụng nó nhằm mục đích gây hại cho khách hàng của chúng ta.

Nếu bạn mã hóa mật khẩu thì nên sử dụng những thuật toàn mạnh mẽ như SHA- 2, nó sẽ sớm trở thành tiêu chuẩn công nghiệp cho bảo vệ mật khẩu. MD5 hay SHA - 1 đã lỗi thời và có thể bị giải mã.
Không lưu những thông tin nhạy cảm nên không thực sự cần thiết.

Bất kì đâu bạn lưu trữ thông tin trong cơ sở dữ liệu, nó cũng có thể gây hại cho khổ chủ nếu chúng rơi vào tay kẻ xấu, nên tốt nhất đừng lưu trữ nó nếu có thể.
Kết luận

SQL injection vẫn tồn tại xung quanh ta trong nhiêu thập kỉ và có khả năng vẫn sẽ tiếp tục thống trị bảng xếp hạng những kiểu tấn công nguy hiểm trong nhiều năm tới. Chúng ta vẫn cần phải luôn chuẩn bị những công cụ để bảo về website của chúng ta khi một ngày nào đó nó ghé thăm.

Hi vọng bài viết của mình sẽ giúp ích cho các bạn.
