
Sau một thời gian dài phát triển với nhiều phiên bản thử nghiệm, Rails 5.0, với hàng trăm lập trình viên góp sức, hàng nghìn commits đã thực sự trở thành một trong những version Rails ổn định và hoàn thiện nhất từ trước tới nay. Rails 5.0 ra đời chứng tỏ cộng động Rails vẫn duy trì và phát triển rất mạnh mẽ. 

Trong Rails 5, có 2 chức năng chính mà chúng ta cần biết:

## Action Cable

Action Cable là phương thức hoàn toàn mới để thực hiện lập trình WebSockets trong Rails. Action Cable là giải pháp tích hợp toàn diện khi nó vừa quản lý các kết nối, kênh truyền từ phía server, đồng thời tầng JavaScript cho các tương tác phía client. Được thiết kế với mục đích đơn giản hóa các tính năng như chat, thông báo, trạng thái online và rất nhiều trường hợp xử lý thời gian thực khác.

Điều thật sự đặc biệt trong Action Cable là khả năng sử dụng hoàn toàn Active Record khi lập trình Websocket. Chúng ta thậm chí có thể sử dụng ActionController::Renderer để render templates mà không cần phải ở trong controller action, khi chúng ta muốn tái sử dụng các template phía server cho responses của Websocket.

Action Cable chạy cùng với ứng dụng, vì vậy chúng ta cần chuyển đổi việc sử dụng development server từ Webrick sang Puma, web server cho phép chạy song song các quá trình.

## API mode

Rails không chỉ là sự lựa chọn hoàn hảo khi bạn muốn xây dựng một ứng dụng full-stack, mà với phiên bản 5.0, Rails còn có khả năng xây dựng ứng dụng backend trả về JSON, cắt bỏ code phía client. Rails 5 giờ còn giúp cho công việc này trở nên dễ dàng hơn với -api mode. Ví dụ
```
rails new backend --api
```
sẽ tạo ra ứng dụng Rails để bạn làm việc với JSON, chứ không phải là HTML

Mạc dù API mode đang phụ thuộc vào phương thức to_json, bạn hoàn toàn có thể sử dụng kết hợp với Jbuilder, Active Model Serializers

## Một số đặc điểm khác
```
can now be written much more succinctly as this: User.left_outer_joins(:orders)
```
Rails 5 sử dụng Ruby 2.2 hoặc cao hơn. Trong version này, symbols được thu dọn tự động, giúp tăng đáng kể hiệu suất quản lý bộ nhớ.
Sử dụng bin/rails db:migrate thay cho bin/rake db:migrate
ApplicationRecord trở thành parent class của tất cả models được tạo bởi generators

### Cho phép gọi view mà không cần phải ở trong controller

```ruby
ApplicationController.render template: 'orders/index.html.erb'
```
In Rails 5, mọi app được tạo ra đều có folder app/jobs chứa file application_job.rb. Mọi class job mới đều kế thừa từ ApplicationJob class.

## Support MySQL JSON data type

```ruby
class CreateUsers < ActiveRecord::Migration 
  def change 
    create_table :user do 
      |t| t.json :settings 
    end 
  end 
end

user.settings = { colours: ["red", "green"], alerts: true }
```
## Left outer join

### Trước kia

```ruby
User.joins("LEFT OUTER JOIN orders ON orders.user_id = users.id") 
```
### Rails 5

```ruby
User.left_outer_joins(:orders)
```
Validation Error Details trong Rails 5 giới thiệu cách trả về errors khi không thỏa mãn validations đặc biệt hữu ích với các API
```ruby
class User < ActiveRecord::Base 
  validates :email, presence: true, length: { in: 5..255 } 
end

## Rails validation check
user = User.new
user.valid? #=> false 
user.errors.details #=> {:email=>[{:error=>:blank}, {:error=>:too_short, :count=>5}]}
```
