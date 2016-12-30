Trong dự án  này, chúng ta sẽ tạo một project cho phép user chat realtime sử dụng Faye, Publish - Subscribe message system dành cho Rails và Nodejs

Publish - Subscribe pattern: Có nghĩa là các client sẽ subscribe (đăng kí) để có thể tiếp nhận những thay đổi từ publishers ( phía tạo ra thay đổi ). Và khi một người dùng publish ( thông báo ) ngay sau khi tạo ra một update, các thông báo đó sẽ gần như ngay lập tức được gửi tới các subscribers, nhờ đó mà quá trình gửi - nhận thông điệp giữa publisher và subscriber diễn ra gần rất nhanh, và liên tục.

## Khởi tạo dự án:

```ruby
rails new mini-chat
```

Vì Faye sẽ chỉ làm việc với Thin Web Server, chứ không phải WEBrick, nên chúng ta sẽ cài đặt Thin Web Server cùng với gem Faye cho dự án

Gemfile

```ruby
gem 'faye-rails', '~> 2.0`
gem 'thin'
```

Add đoạn code sau vào application.rb

```ruby
config.middleware.delete Rack::Lock
config.middleware.use FayeRails::Middleware, mount: '/faye', :timeout => 25
```

=> Chúng ta cho Rails biết sẽ sử dụng Faye như một middleware (tầng kiến trúc / phần mềm giúp gắn kết các tầng / phần / phần mềm lại với nhau)

## Require Faye js

application.js

```javascript
//= require faye
```

Để khởi động dự án, chúng ta dùng lệnh

```
$ thin start
```

Để xem log dự án trong terminal ( hoặc tab khác )

```
$ tail log/development.log -f -n 200
```

## Tạo Comment resource

```ruby
rails g scaffold Comment content:text

rake db:migrate
```

Nếu bạn sử dụng gem Tuborlink nhưng lại chưa add gem jquery-turbolink thì hãy thêm gem này, nếu không default function Jquery.ready() sẽ không hoạt động

## Gemfile 

```ruby
gem 'jquery-turbolinks'
```

application.js

```javascript
//= require jquery.turbolinks
//= require turbolinks
```

## Edit views

views/comments/index.html.erb

```ruby
<h1>Join the discussion</h1>

<%= render 'form' %>

<div id="comments">
    <ul class="media-list">
      <%= render @comments %>
    </ul>
</div>
```

views/comments/_comment.html.erb

```ruby
<p><%= comment.content %></p>
```

views/comments/_form.html.erb 

```ruby
<%= form_for @comment, remote: true do |f| %>
      <div>
        <%= f.label :content, 'Enter your comment:' %>
        <%= f.text_area :content, rows: 3, required: true, maxlength: 2000 %>
        <small class="label label-warning">Cannot be blank or contain more than 2000 symbols.</small>
      </div>

      <%= f.submit 'Submit'%>
<% end %>
```
## Tạo file comments.coffee

```javascript
window.client = new Faye.Client('/faye')

jQuery ->
  client.subscribe '/comments', (payload) ->
    $('#comments').find('.media-list').prepend(payload.message) if payload.message
```
=> Chúng ta đang tạo một Faye client subscribe kênh '/comments'. Mỗi khi có comment mới truyền tới kênh đó, chúng ta sẽ chèn nội dung comment vào list các comment

## Require comments js

application.js
```javascript
//= require faye
//= require comments
```
Do form của chúng ta đang sử dụng remote form, tức là khi submit, comments#create sẽ gọi file create.js.erb. Khi đó, chúng ta sẽ publish comment lên kênh /comments, là kênh mà file list các comments đang subscribe.

comments/create.js.erb
```javascript
publisher = client.publish('/comments', {
  message: '<%= j render @comment %>'
});
```
=> Publisher sẽ truyền <%= @comment %> sau khi được biên dịch sang html code, và truyền tới kênh /comments
 j là cách gọi tắt của escape_javascript, dùng để render partial trong file js

Update trạng thái của button post khi tạo comment

```javascript
 jQuery ->
  client.subscribe '/comments', (payload) ->
    $('#comments').find('.media-list').prepend(payload.message) if payload.message

  $('#new_comment').submit -> $(this).find("input[type='submit']").val('Sending...').prop('disabled', true)
```
Sử dụng Faye callback để update trạng thái của button Submit và xóa dữ liệu nhập tại ô text

views/comments/create.js.erb
```ruby
publisher.callback(function() {
  $('#comment_body').val('');
  $('#new_comment').find("input[type='submit']").val('Submit').prop('disabled', false)
});

publisher.errback(function() {
  alert('There was an error while posting your comment.');
});
```
## Update controller

controllers/comments_controller.rb
```ruby
def index
    @comment = Comment.new
    @comments = Comment.all
end

def create
    @comment = Comment.create(comment_params)
end
```
## Upload to Heroku

Để có thể upload dự án lên heroku, các bạn tạo  file Procfile trong thư mục chính dự án và thêm nội dung

```ruby
web: bundle exec rails server thin -p $PORT -e $RACK_ENV
```
và add gems cho môi trường production
```ruby
group :production do
  gem 'rails_12factor'
  gem 'pg'
end
```
