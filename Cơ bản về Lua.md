# NGHIÊN CỨU NGÔN NGỮ LẬP TRÌNH LUA
Bên dưới là những kết quả nghiên cứu ngôn ngữ lập trình LUA. Gồm những nội dung chính sau:
- Đặc trưng của ngôn ngữ lập trình LUA.
- So sánh khả năng biểu diễn với các ngôn ngữ lập trình khác cùng họ scripting.
- So sánh hiệu năng với các ngôn ngữ lập trình khác cùng họ scripting.

## ĐẶC TRƯNG CỦA NGÔN NGỮ LUA
### Tính mở rộng:
 
-Người ta không chỉ quan tâm đến LUA như một ngôn ngữ, mà còn như là một công cụ dùng để xây dựng một ngôn ngữ.
-Những chương trình viết bằng LUA được thiết kế từ đầu, sau này có thể được mở rộng không chỉ bằng chính ngôn ngữ LUA mà còn cả ngôn ngữ C.
-LUA dễ dàng giao tiếp với ngôn ngữ C/C++ và những ngôn ngữ khác như: Fortran, Java, Smalltalk, Ada, và thậm chí với những ngôn ngữ scripting khác.
 
### Tính đơn giản:
 
-LUA là một ngôn ngữ đơn giản và nhỏ. Nó có rất ít các khái niệm, kiểu dữ liệu … nhưng lại rất mạnh.
-Tính đơn giản làm cho LUA rất dễ học và dễ tích hợp vào những chương trình lớn khác.
-Một chương trình đầy đủ của LUA bao gồm: mã nguồn, hướng dẫn, cộng với một vài thư viện nhị phân tương ứng cho platforms, có thể sắp xếp gọn trong một đĩa mềm.
 
### Tính hiệu quả:
 
-Chương trình được viết bằng LUA thực thi khá nhanh.
-LUA được đánh giá như một trong những ngôn ngữ nhanh nhất trong lĩnh vực của những ngôn ngữ scripting.
 
### Tính khả chuyển:
 
-LUA không chỉ chạy tốt trên Windows và Unix. LUA còn chạy tốt trên mọi platforms mà chúng ta biết đến như : NextStep, OS/2, PlayStation II (Sony), Mac OS-9 and OS X, BeOS, MS-DOS, IBM mainframes, EPOC, PalmOS, MCF5206eLITE Evaluation Board, RISC OS.
-Với cùng một mã nguồn có thể chạy trên nhiều môi trường khác nhau. Bởi vì LUA được cài đặt theo chuẩn ANSI C nên nếu có một ANSI compiler thì có thể compile LUA.
 
### Tính “đa dạng thức”:
 
-LUA có cấu trúc đơn giản nhưng giải quyết được nhiều vấn đề phức tạp khác nhau, trong khi những ngôn ngữ khác có cấu trúc phức tạp nhưng chỉ giải quyết một vấn đề chuyên biệt.
-LUA không có tính kế thừa nhưng cho phép tạo ra mối quan hệ đó với metatable (*).
-Cho phép người lập trình tạo namespaces, class và những đặc tính liên quan khác sử dụng sự thi hành của table.
 
### Thư viện dễ thay đổi:
 
-Có thể mở rộng các kiểu dữ liệu và các hàm của thư viện.
-Có bộ nhớ tự động nên không cần quan tâm ai là người cấp phát và giải phóng bộ nhớ hay là tràn bộ nhớ.
-Những hàm đặc biệt cho phép sự thể hiện của các tham số ở mức độ cao nên có thể tạo các hàm có nhiều chức năng hơn.
-Khi ghi chương trình LUA vào vi xử lý, do phần cứng bị hạn hẹp ta có thể vào trong thư viện của LUA để loại bỏ những hàm không cần thiết.
 
### Tính tích hợp:
 
-Sử dụng LUA để tích hợp vào trong chương trình ứng dụng của mình.
-Sử dụng trong CGILUA để xây dựng một trang web động.
-Sử dụng LuaOrb, cho việc truy cập những đối tượng CORBA.
-Sử dụng LUA-C API để tạo ra những hàm mới, kiểu dữ liệu mới, thay đổi cách hoạt động của một vài hệ thống ngôn ngữ, cấu hình LUA cho những phân vùng đặc biệt của chúng.
 
### Table là kiểu dữ liệu “mạnh”:
 
-Tạo các key trong table rất đơn giản
-Thay đổi cấu trúc và chỉ mục của table đã được tạo trước.
-Có thể sử dụng table như 1 mảng
-Sử dụng vòng lặp trong table
-Viết chương trình hướng đối tượng với table.
-Xây dựng những cấu trúc dữ liệu từ table.
-Những phương thức được định nghĩa sẳn trên table:
oTable.insert: thêm một phần tử vào table
**Ví dụ:**
```lua        
T = {}
table.insert(T, “a”)
table.insert(T, “b”)
table.insert(T, “c”)
print(CommaSeparate(T)) 
a, b, c
```
oTable.sort : sắp xếp các phần tử trong 1 table
**Ví dụ sử dụng chức năng sort :**
```lua
Names =  {“Scarlatti”, “Telemann”, “Corelli”, “Purcell”,
          “Vivaldi”,  “Handel”, “Bach”}
table.sort(Names)
for I, Name in ipairs(Names) do
          print(I,  Name)
end
```
Trích:
```
1 Bach
2 Corelli
3 Handel
4 Purcell
5 Scarlatti
6 Telemann
7 Vivaldi 
```
oTable.concat: nối các phần tử trong table thành một chuổi.
**Ví dụ :**
```lua
print(table.concat({“a”, “bc”, “d”}))
-- Abcd
```
oTable.remove: Remove một phần tử trong table.
**Ví dụ:**
```lua
T = {}
table.insert(T, “a”)
table.insert(T, “b”)
table.insert(T, “c”)
print(CommaSeparate(T))
a, b, c
print(table.remove(T))
c
print(CommaSeparate(T))
a, b
print(table.remove(T))
b
print(CommaSeparate(T))
a
print(table.remove(T))
a 

-- T is now empty again:
print(#T)
```
oTable.maxn: tìm trên mỗi cặp key – value trong một table và trả về key tương ứng với value lớn nhất hoặc trả về 0 nếu value không phải là số dương.
**Ví dụ:**
```lua
print(table.maxn({“a”, nil, nil, “c”}))
-- 4
print(table.maxn({[1.5] = true}))
-- 1.5
print(table.maxn({[ì1.5î] = true}))
-- 0 
```
### Mở rộng các xử lý trên table bằng Metatable
 
-Mỗi table có thể là một metatable.
-Mỗi table có 1 cặp key-value. Mỗi metatable có 1 cặp event-metamethod. Một event ứng với 1 key trong table và metamethod ứng với 1 value trong table. Mỗi metatable có thể có 1 hoặc nhiều table và ta có thể tính toán được trên metatable dựa vào metamethod.
-Metamethod giống như 1 hàm tính toán trong metatable.
-Ví dụ, sử dụng metatable chúng ta có thể định nghĩa trong ứng dụng Lua việc tính toán biểu thức a+b như thế nào, trong đó a và b là các table.
-Mỗi một table có thể là một metatable của bất kỳ một table khác. Một nhóm các table có liên quan với nhau có thể chia sẻ một metatable (cái mà diễn tả xử lý chung của chúng).
 
### Mở rộng với Function:
 
-Khai báo hai biến cùng tên trong cùng một khối lệnh. Ví dụ:
```lua
function ScopeTest3(Lcl)
    for I = 1, 5 do
        Lcl = Lcl .. "a"
        print(Lcl)
        local Lcl =  ""
        Lcl = Lcl ..  "z"
        print(Lcl)
    end
    print("Kết  quả sau vòng lặp.")
    print(Lcl)
end
ScopeTest3("") 
```
Kết quả:
```
a
z
aa
z
aaa
z
aaaa
z
aaaaa
z
```
Kết quả sau vòng lặp.
```
aaaaa
```
- Định nghĩa function như gán giá trị
```lua
DoNothing1, DoNothing2 = function() end, function() end
print(DoNothing1, DoNothing2)
print(DoNothing1 == DoNothing2) 

-- Kết quả:
function: 011540E0 function: 01154080
false
```
- Định nghĩa và gọi 1 hàm nặc danh (anonymous function)
```lua
(function(A, B)
print(A + B)
end)(2, 3)
--Kết quả: 5
```
- Định nghĩa và gọi hàm cục bộ
```lua
  do
      local LclAverage = function(Num1, Num2)
      return (Num1 + Num2) / 2
  end
  print(LclAverage(10, 20))
  end 
     
-- Kết quả: 15
```
- Gọi hàm không cần truyền đúng số lượng đối số như khi định nghĩa
```lua
  function Output(a,b,c)
      print (a,b,c)
  end
  Output(1,2) 
     
-- Kết quả:
1 2 nil
```
- Định nghĩa nhiều hàm con trong 1 hàm cha, có thể gọi những hàm con này từ bên ngoài hàm cha
```lua
    function A()
      for I = 1, 2 do
          if I == 1  then
              function  One()
                    return I
              end
          else
              function  Two()
                    return I
              end
          end
      end
  end
  print(A())
  print(One())
  print(Two()) 
     
-- Kết quả :
1
2
```
- Tạo và khởi tạo nhiều biến local cùng 1 lúc.
```lua
  do
      local A, B = 1, 2
      print(A, B)
      local A, B = 1
      print(A, B)
      local A, B = 1,  2, 3
      print(A, B)
  end 
```
- Giá trị trả về của hàm là một hàm.Ví dụ:
- Trả lại hai chức năng: một chức năng là lấy giá trị của N và một chức năng làm tăng giá trị N bởi đối số của nó.
```lua
function MakeGetAndInc(N)
  -- Trả về giá trị N:
  local function Get()
  return N
end
```
-- Tăng N bởi M:
```lua
      local function  Inc(M)
          N = N + M
      end
      return Get, Inc
  end 
     
-- Tạo 2 cặp hàm Get và Inc, một cặp khởi tạo 0 và 1 cặp khởi tạo 100:
  GetA, IncA = MakeGetAndInc(0)
  GetB, IncB = MakeGetAndInc(100) 
  -- Xuất ra màn hình:
  print(GetA())
  print(GetB())
  IncA(5)
  print(GetA())
  IncA(5)
  print(GetA())
  IncB(1)
  print(GetB())
  print(GetA())
  IncA(1) 
```
**Kết quả:**
```
0
100
5
10
101
10
```
### Lập trình cho web:
 
-Lập trình web động:
-Thực thi CGI Script
-Xây dựng ứng dụng CGI tương tác
 
### Viết chương trình game với LUA:
 
-Viết các phần mềm game 2D sử dụng SDL.
-Viết các phần mềm game 3D sử dụng OPENGL.

Để bắt đầu so sánh LUA với các ngôn ngữ lập trình khác cùng họ (scripting), luận văn này đã chọn ra 2 ngôn ngữ lập trình khác mà theo đánh giá thu thập được qua các trang web và của “giới lập trình” hiện nay là rất chiếm ưu thế - đó là Python và Ruby.
 
# SO SÁNH SYNTAX VỚI CÁC NGÔN NGỮ LẬP TRÌNH KHÁC CÙNG HỌ SCRIPTING
 
Trong chương này, luận văn sẽ so sánh về syntax của ngôn ngữ Lua với hai ngôn ngữ cùng họ là Python và Ruby.
 
## Biểu diễn toán học và các hàm đại số
 
### Các phép toán:
 
Cả 3 ngôn ngữ đều hỗ trợ các phép toán sau:
 
-Cộng (+)
-Trừ (-)
-Nhân(*)
-Chia (/)
 
-Gán (=)
-So sánh bằng (==)
-Lớn hơn (>)
-Nhỏ hơn (<).
 
### Các hàm đại số:
 
-Logical NOT or Not Equal To
-Logical AND
-Logical OR
-Square Root
-Exponent
-Absolute Value
-Basic Sin
-Cosin
-Tangent
-Logarithm
-Truncate/Round
-Floor
-Ceiling
-Power

**Kết luận:**
Cả ba ngôn ngữ Python, Ruby, LUA có cùng khả năng biểu diễn các phép toán đại số và các biểu thức toán học.
|---|---|---|---|---|---|
| STT | Kiểu dữ liệu và giá trị | Python | Ruby | Lua | Nhận xét|
|---|---|---|---|---|---|
1.
Nil
X
X
X
 
2.
Booleans
X
X
X
 
3.
Numbers
X
X
X
 
4.
Strings
X
X
X
 
5.
Tables
 
 
X
 
6.
Functions
 
 
X
 
7.
Userdata and Threads
 
 
X
 
8.
Mảng 1 chiều
X
X
X
 
9.
Mảng 2 chiều
X
X
X
 
10.
Mảng n chiều
X
X
X
 
11.
Dữ liệu cấu trúc
X
X
X
 
12.
Danh sách liên kết
X
X
X
 
13.
Cấu trúc dữ liệu cây
 
X
X
 
14
Queuse and Double Queues
X
X
X
 
15
Sets và Bags
 
X
X
 
16
String Buffer
 
 
X
 
3.2.Biểu diễn các kiểu dữ liệu
 
Bảng 1: So sánh biểu diễn các kiểu dữ liệu của 3 ngôn ngữ (Lua, Python, Ruby).
 
 
 
Kết luận:
Khả năng biểu diễn các kiểu dữ liệu cơ sở và có cấu trúc của LUA không thua kém Python và Ruby. Hơn nữa, LUA còn có thế mạnh của các kiểu dữ liệu đó là function và tables. Đặc biệt là tables, kiểu dữ liệu này rất dễ biểu diễn và có thể thay cho nhiều kiểu dữ liệu có cấu trúc khác như mảng, danh sách liên kết…
 
3.3.Biểu diễn xử lý:
 
 
STT
Khả năng biểu diễn xử lý
Python
Ruby
Lua
Nhận xét
1.
Rẽ nhánh đơn
X
X
X
 
2.
Rẽ nhánh kép
X
X
X
 
3.
Vòng lặp Numeric For
X
X
X
 
4.
Vòng lặp Generic For
X
X
X
 
5.
Vòng lặp While
X
X
X
 
6.
Vòng lặp Repeat … Until
 
 
X
 
7.
Vòng lặp vĩnh viễn
X
X
X
 
8.
Lặp từ giá trị đầu đến giá trị cuối theo từng bước
X
X
X
 
9.
Lặp từng biến trong danh sách biến
X
X
X
 
 
Bảng 2: So sánh biểu diễn xử lý của 3 ngôn ngữ (Lua, Python, Ruby).
 
 
Kết luận:
Về biểu diễn xử lý, với những cấu trúc rẻ nhánh, các biểu diễn vòng lặp, ba ngôn ngữ này có khả năng biểu diễn tương đương nhau.
 
3.4.Biểu diễn FUNCTION
 
STT
Khả năng biểu diễn
Python
Ruby
Lua
Nhận xét
1.
Định nghĩa function
X
X
X
 
2.
Return nhiều giá trị
X
 
X
 
3.
Khai báo 2 biến cùng tên trong cùng khối lệnh
 
 
X
 
4.
Gọi đệ quy
X
X
X
 
5.
So sánh 2 functions như 2 biến
 
 
X
 
6.
Định nghĩa function như gán giá trị
 
 
X
 
7.
Định nghĩa và gọi 1 hàm nặc danh (anonymous function)
 
 
X
 
8.
Định nghĩa và gọi hàm cục bộ
 
 
X
 
9.
Tạo 1 function bằng cách gọi từ 1 function khác
 
 
X
 
10.
Gọi hàm không cần truyền đúng số lượng đối số như khi định nghĩa
 
 
X
 
11.
Định nghĩa nhiều hàm con trong 1 hàm cha, có thể gọi những hàm con này từ bên ngoài hàm cha
 
 
X
 
12.
Khi định nghĩa function, các tham số được phép gán mặc định
X
 
X
 
13.
Return giá trị từ function định nghĩa
 
 
X
 
14
Return no value
X
 
X
 
 
Bảng 3: So sánh biểu diễn FUNCTION của 3 ngôn ngữ (Lua, Python, Ruby).
 
 
Kết luận:
Khả năng biểu diễn về hàm của LUA rất phong phú và đa dạng. Đặc biệt có thể định nghĩa nhiều hàm con trong 1 hàm cha, và lợi thế hơn hẳn là có thể gọi những hàm con này từ bên ngoài hàm cha.
 
3.5.Biểu diễn CLASS
 
STT
Khả năng biểu diễn
Python
Ruby
Lua
Nhận xét
1.
Định nghĩa class
X
X
X
 
2.
Cho phép thiết lập kế thừa
X
X
X
 
3.
Cho phép thiết lập đa kế thừa
X
 
X
 
4.
Các method trong 1 class có thể trùng tên
 
 
X
 
5.
Các properties trong 1 class có thể trùng tên
 
 
X
 
 
Bảng 4: So sánh biểu diễn CLASS của 3 ngôn ngữ (Lua, Python, Ruby).
 
 
Kết luận:
Khả năng biểu diễn class của LUA đa dạng hơn hẳn Python và Ruby. Tuy LUA không hỗ trợ sẵn nhưng cho phép người dùng có thể thiết lập quan hệ kế thừa, đặc biệt là đa kế thừa.
 
 
 
 
 
Chương 4: SO SÁNH HIỆU NĂNG VỚI CÁC NGÔN NGỮ LẬP TRÌNH KHÁC CÙNG HỌ SCRIPTING
 
 
Khi so sánh các ngôn ngữ lập trình thì tốc độ thực thi là một trong những khía cạnh không thể thiếu.
Tuy nhiên, rất khó so sánh ở mức tổng quát, và điều này nếu có làm được cũng vượt ngoài phạm vi của luận văn.
Trong luận văn này, chỉ cố gắng minh họa sự vượt trội của LUA thông qua một số ví dụ điển hình.
Cách so sánh qua ví dụ :
•Chọn các bài toán điển hình trong các lĩnh vực của lập trình: Đệ quy, đồ họa, game, tính toán với khối lượng lớn, mô hình client/server …
•Định nghĩa thuật toán cho ví dụ minh họa.
•Cài đặt cùng một thuật toán (cho cùng một bài toán) trong những ngôn ngữ lập trình cần so sánh khác nhau. Cố gắng đảm bảo có sự tương đồng về syntax trong các cài đặt.
“Sự tương đồng về syntax” được hiểu như sau:
•Syntax: Ví dụ như cùng một kiểu vòng lặp for trong các ngôn ngữ khác nhau thì cố gắng biểu diễn trong hai ngôn ngữ đều cùng một kiểu vòng for)
Phương thức so sánh trên mang tính tương đối, vì tốc độ thực thi phụ thuộc vào rất nhiều các yếu tố sau đây :
•Ngôn ngữ cài đặt.
•Trình biên dịch tương ứng.
•Môi trường thực thi.
•Bài toán dùng để so sánh
•Cách thức cài đặt (sự tương đồng về syntax).
Bởi vậy, phương thức so sánh này thiếu tính khoa học, chỉ mang tính “minh họa để thuyết phục”.
 
4.1.So sánh tốc độ thực thi của 3 ngôn ngữ qua các cấu trúc điều khiển cơ bản
 
-Vì thời gian thực hiện 1 lệnh rất bé không thể nhìn thấy được tốc độ thực thi của nó vì thế để biết được tốc độ thực thi của từng dòng lệnh ứng với từng ngôn ngữ ta phải để chúng nằm trong vòng lặp với số lần lặp tương đối lớn.
-Với N = 1000.000 ta có thể thấy được sự khác biệt về tốc độ thực thi của từng dòng lệnh ứng với từng ngôn ngữ.
-Kết quả của các chương trình minh họa bên dưới được thực trên máy tính có cấu hình như sau:
•CPU: Pentium Dual-Core T2080 1.73GHz, 1MB L2 cache.
•RAM: 2GB DDR2.
•Hệ điều hành: Window Vista Ultimate.
-Kết quả bên dưới chỉ mang tính tương đối và tùy thuộc vào môi trường lúc thực thi chương trình.
 
4.1.1.Vòng lặp for:
 
4.1.1.1.Source code ví dụ:
 
a.LUA:
    Code:         
    function VongFor()
      for i = 1,N do
          j = 1
      end
  end
 
  print "Vong lap for:"
  local x = os.clock()
  VongFor()
  print(string.format("elapsed time: %.2f  seconds\n", os.clock() - x)) 
     
b.Python:
    Code:         
    N  = N + 1
  def VongFor():
      for i in  range(1,N):
          j = 1
   
  print "Vong lap for:"
  t1 = time.clock()
  VongFor()
  t2 = time.clock()
  print "elapsed time: ",  t2-t1 
     
c.Ruby:
    Code:         
    def VongFor()
      for i in 1..N do
          j = 1
      end
  end 
     
    Code:         
      print "Vong lap for:\n"
  t1 = Time.now
  VongFor()
  t2 = Time.now
  print "Elapsed time: %0.2f" % (t2-t1).to_f,  " seconds\n" 
     
4.1.1.2.Nhận xét kết quả:
 
 
Ngôn ngữ
LUA
Python
Ruby
Nhận xét
N = 1,000,000
0.09s
0.17s
0.36s
LUA nhanh nhất
 
4.1.2.Vòng lặp while nằm ngoài function:
 
4.1.2.1.Source code ví dụ:
 
a.LUA:
    Code:         
    print("Vong while ngoai function:")
  local x = os.clock()
  i = 1
  while  (i<=N) do
      i = i+1
  end
  print(string.format("elapsed time: %.2f  seconds\n",os.clock() - x)) 
     
b.Python:
    Code:         
    x = time.clock()
  i = 1
  while (i<=N) :
      i = i+1
  print "Vong lap while ngoai function:"
  print "elapsed time: ",time.clock() – x 
     
c.Ruby:
    Code:         
              t1 = Time.now
  i = 1
  while (i<=N) do
      i = i+1
  end
  t2 = Time.now
  print "Vong lap while ngoai function:\n"
  print "Elapsed time: %0.2f" % (t2-t1).to_f,  " seconds\n" 
     
4.1.2.2.Nhận xét kết quả:
 
 
Ngôn ngữ
LUA
Python
Ruby
Nhận xét
N = 1,000,000
0.31s
0.43s
1.08s
LUA nhanh nhất
 
4.1.3.Vòng lặp while nằm trong Function:
 
4.1.3.1.Source code ví dụ:
 
a.LUA:
    Code:         
    function VongWhile()
      i = 1
      while (i<=N)  do
          i = i+1
      end
  end 
     
    Code:         
    print "Vong lap while trong function:"
  local x = os.clock()
  VongWhile()
  print(string.format("elapsed time: %.2f  seconds\n", os.clock() - x)) 
     
b.Python:
    Code:         
    def VongWhile():
      i = 1
      while (i<=N):
          i = i+1
 
  print "Vong lap while trong function:"
  t1 = time.clock()
  VongWhile()
  t2 = time.clock()
  print "elapsed time: ",  t2-t1 
     
c.Ruby:
    Code:         
    def VongWhile()
      i = 1
      while (i<=N)  do
          i = i+1
      end
  end
  print "Vong lap while trong function:\n"
  t1 = Time.now
  VongWhile()
  t2 = Time.now
  print "Elapsed time: %0.2f" % (t2-t1).to_f,  " seconds\n" 
     
 
4.1.3.2.Nhận xét kết quả:
 
 
Ngôn ngữ
LUA
Python
Ruby
Nhận xét
N = 1,000,000
0.33s
0.20s
1.09s
Python nhanh nhất, nhưng LUA nhanh hơn Ruby
 
Nhận xét:
Trong LUA, khi đặt vòng lặp “While” trong function sẽ chậm hơn Python. Vì vậy khi lập trình trong LUA hạn chế sử dụng vòng lặp “While” để tính thực thi của LUA cao hơn.
 
4.1.4.Cấu trúc điều kiện:
 
4.1.4.1.Source code ví dụ:
 
a.LUA:
 
function CauTrucDieuKien()
for i = 1,N do
if (i<N) then
j = 1
else
j = 1
end
end
end
print "Cau Truc Dieu Kien:"
local x = os.clock()
CauTrucDieuKien()
print(string.format("elapsed time: %.2f seconds\n", os.clock() - x))
 
b.Python:
 
N = N + 1
def CauTrucDieuKien():
for i in range(1,N):
if (i<N):
j = 1
else:
j = 1
print "Cau Truc Dieu Kien:"
t1 = time.clock()
CauTrucDieuKien()
t2 = time.clock()
print "elapsed time: ", t2-t1
 
c.Ruby:
 
def CauTrucDieuKien()
for i in 1..N do
if (i<N) then
j = 1
else
j = 1
end
 
end
end
print "Cau Truc Dieu Kien:\n"
t1 = Time.now
CauTrucDieuKien()
t2 = Time.now
print "Elapsed time: %0.2f" % (t2-t1).to_f, " seconds\n"
 
4.1.4.2.Nhận xét kết quả:
 
 
Ngôn ngữ
LUA
Python
Ruby
Nhận xét
N = 1,000,000
0.22s
0.24s
0.84s
LUA nhanh nhất
 
4.1.5.Biểu thức toán học:
 
4.1.5.1.Source code ví dụ:
 
a.LUA:
 
function BieuThucToanHoc()
for i = 1,N do
a = (i+1)-(i/2)*2 + math.sqrt(5)
end
end
print "Bieu thuc toan hoc:"
local x = os.clock()
BieuThucToanHoc()
print(string.format("elapsed time: %.2f seconds\n", os.clock() - x))
 
b.Python:
 
N = N + 1
def BieuThucToanHoc():
for i in range(1,N):
a = (i+1)-(i/2)*2 + math.sqrt(5)
print "Bieu thuc toan hoc:"
t1 = time.clock()
BieuThucToanHoc()
t2 = time.clock()
print "elapsed time: ", t2-t1
 
c.Ruby:
 
def BieuThucToanHoc()
for i in 1..N do
a = (i+1)-(i/2)*2 + Math.sqrt(5)
end
end
 
print "Bieu thuc toan hoc:\n"
t1 = Time.now
BieuThucToanHoc()
t2 = Time.now
print "Elapsed time: %0.2f" % (t2-t1).to_f, " seconds\n"
 
4.1.5.2.Nhận xét kết quả:
 
 
Ngôn ngữ
LUA
Python
Ruby
Nhận xét
N = 1,000,000
0.48s
1.44s
3.65s
LUA nhanh nhất
 
4.1.6.Biểu thức logic:
 
4.1.6.1.Source code ví dụ:
 
a.LUA:
 
function BieuThucLogic()
for i = 1,N do
a = (i and 1) or (i)
end
end
 
print "Bieu thuc logic:"
local x = os.clock()
BieuThucLogic()
print(string.format("elapsed time: %.2f seconds\n", os.clock() - x))
 
b.Python:
 
N = N + 1
def BieuThucLogic():
for i in range(1,N):
a = (i and 1) or (i)
 
print "Bieu thuc logic:"
t1 = time.clock()
BieuThucLogic()
t2 = time.clock()
print "elapsed time: ", t2-t1
 
c.Ruby:
 
def BieuThucLogic()
for i in 1..N do
a = (i and 1) or (i)
end
end
 
print "Bieu thuc logic:\n"
t1 = Time.now
BieuThucLogic()
t2 = Time.now
print "Elapsed time: %0.2f" % (t2-t1).to_f, " seconds\n"
4.1.6.2.Nhận xét kết quả:
 
 
Ngôn ngữ
LUA
Python
Ruby
Nhận xét
N = 1,000,000
0.12s
0.28s
0.47s
LUA nhanh nhất
 
Ngoài những cấu trúc điều khiển mà cả 3 ngôn ngữ lập trình trên đều có. LUA còn có thêm những cấu trúc mà Python và Ruby không có:
 
4.1.7.Vòng lặp repeat..until:
 
4.1.7.1.Source code ví dụ:
 
a.LUA:
function VongRepeat()
i = 0
repeat
i = i+1
until (i>N)
end
 
print "Vong lap repeat:"
local x = os.clock()
VongRepeat()
print(string.format("elapsed time: %.2f seconds\n", os.clock() - x))
 
Nhận xét chung:
Trong 5 chương trình nêu trên, tỷ lệ số chương trình mà mỗi ngôn ngữ chiếm ưu thế như sau:
-LUA: 4/5 = 80%
-Python: 1/5 = 20%
-Ruby: 0/5 = 0%
Như vậy có thể kết luận, LUA chiếm ưu thế hơn hẳn trong 3 ngôn ngữ này. Và vì đây là những cấu trúc điều khiển cơ bản của ngôn ngữ nên có thể suy ra điều này đúng với các chương trình lớn cũng như các hệ thống xử lý phức tạp khác được xây dựng trên một trong 3 ngôn ngữ LUA, Python, Ruby.
 
4.2.So sánh qua các bài toán thông dụng
 
Các bài toán được chọn sau đây điển hình trong các lĩnh vực: đệ quy, đồ họa, game, mô hình client/server … và thường quen thuộc với mọi đối tượng làm việc trong ngành công nghệ thông tin.
 
4.2.1.Mô tả các bài toán
 
4.2.1.1.Nhóm đệ quy:
 
Bài toán 1: Bài toán Fibonacy.
Mô tả:
Cho 1 giá trị nguyên dương n, tính F (n) với:
F (0) = 1
F (1) = 1
F (2) = F (0) + F (1)
……
F (n) = F (n-2) + F (n-1)
Thuật toán:
 
int Fibonacy(int n)
{
Nếu (n == 1 hoặc n == 2) thì
Trả về 1;
Trả về ( Fibonacy(n-1) + Fibonacy(n-2) );
}
 
Bài toán 2: Bài toán sắp xếp QuickSort.
Mô tả:
Cho 1 dãy số gồm n phần tử. Dùng phương pháp sắp xếp QuickSort để sắp xếp tăng dần dãy phần tử đã cho.
Thuật toán:
 
void quickSort(A, lower, upper)
{
x = A[(lower + upper) / 2];
i = lower;
j = upper;
Làm
{
[i] Trong khi (A < x) thì làm i ++;
Trong khi (A[j] > x) thì làm j --;
Nếu (i <= j) thì
[i] swap(A, A[j]);
i ++;
j --;
Cuối nếu
} Trong khi (i <= j);
 
Nếu (j > lower) thì
quickSort(A, lower, j);
Nếu (i < upper) thì
quickSort(A, i, upper);
}
Lúc gọi hàm :
quickSort(mảng 1 chiều A, chỉ số phần tử đầu của mảng A, chỉ số phần tử cuối của mảng A)
 
 
4.2.1.2.Nhóm đồ họa:
 
Bài toán 3: Bài toán biến hình (2D).
Mô tả:
Xây dựng bài toán biến 1 con hổ thành 1 cô gái và ngược lại.
(Thuật toán ImageTransform)
1 hình nguồn, 1 hình đích, tìm các hình trung gian sao cho show lần lượt các hình trung gian thì cho thấy sự biến đổi “trơn”.
 
 
Thuật toán:
 
Hình 1: Transform từ cô gái thành con hổ
 
 
For each pixel X in the destination
DSUM=0
weightsum = 0
For each line PiQi
calculate u, v based on PiQi
calculate X’i based on u, v and P’iQ’i
calculate displacement Di=X’i-Xi for this line
dist= shortest distance from X to PiQi
weight = (lengthP / (a + dist))b
DSUM += Di * weight
weightsum += weigth
X’ = X + DSUM / weightsum
destinationImage(X) = sourceImage(X’)
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
Hình 2: Kết quả Transform từ cô gái thành con hổ
 
Bài toán 4: Bài toán chuyển động (2D).
Mô tả:
Xây dựng bài toán cho hòn bi lăn từ vị trí A sang vị trí B.
(Nếu khi cài đặt thấy thời gian chạy từ A sang B trên các ngôn ngữ khác nhau thì kết luận hiệu năng của từng ngôn ngữ khác nhau).
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
Hình 4: Chuyển động 2D sử dụng ngôn ngữ Python
 
Thuật toán:
 
for i = 1 … nTimes làm
xImg = xTop
yImg = yTop
for j = 1 … nRound làm
for i = 0 … N làm
img = ChoseImage(i*deSpace)
SDL.SDL_BlitSurface(img, nil, Screen,{x = xImg, y = yImg, w = img.w, h = img.h})
SDL.SDL_UpdateRect(Screen, 0, 0, 0, 0)
 
--rise x and y
xImg = xImg + space
 
-- delay
SDL.SDL_Delay(DELAY)
 
-- Tô màu đen cho ảnh
SDL.SDL_FillRect(Screen,Black)
Cuối for
Cuối for
-- Vẽ quả bóng ở vị trí cuối
img = image0
SDL.SDL_BlitSurface(img, nil, Screen,{x = xImg, y = yImg, w = img.w, h = img.h})
SDL.SDL_UpdateRect(Screen, 0, 0, 0, 0)
Cuối for
Bài toán 5: Bài toán chuyển động (3D).
Mô tả:
Xây dựng bài toán cho Kim tự tháp quay.
 
Hình 5: Chuyển động 3D sử dụng ngôn ngữ Lua
 
 
 
 
 
 
Hình 6: Chuyển động 3D sử dụng ngôn ngữ Python
 
Thuật toán:
 
function DrawScene()
 
gl.Clear(gl.COLOR_BUFFER_BIT, gl.DEPTH_BUFFER_BIT)
 
gl.LoadIdentity()
gl.Translate(-1.5, 0.0, -6.0)
 
-- Quay kim tự tháp trên trục OY
gl.Rotate(rtri, 0.0, 1.0, 0.0)
 
-- Vẽ kim tự tháp
gl.Begin(gl.TRIANGLES)
gl.Color( 1.0, 0.0, 0.0)
gl.Vertex( 0.0, 1.0, 0.0)
gl.Color( 0.0, 1.0, 0.0)
gl.Vertex(-1.0, -1.0, 1.0)
gl.Color( 0.0, 0.0, 1.0)
gl.Vertex( 1.0, -1.0, 1.0)
 
gl.Color( 1.0, 0.0, 0.0)
gl.Vertex( 0.0, 1.0, 0.0)
gl.Color( 0.0, 0.0, 1.0)
gl.Vertex( 1.0, -1.0, 1.0)
gl.Color( 0.0, 1.0, 0.0)
gl.Vertex( 1.0, -1.0, -1.0)
 
gl.Color( 1.0, 0.0, 0.0)
gl.Vertex( 0.0, 1.0, 0.0)
gl.Color( 0.0, 1.0, 0.0)
gl.Vertex( 1.0, -1.0, -1.0)
gl.Color( 0.0, 0.0, 1.0)
gl.Vertex(-1.0, -1.0, -1.0)
 
gl.Color( 1.0, 0.0, 0.0)
gl.Vertex( 0.0, 1.0, 0.0)
gl.Color( 0.0, 0.0, 1.0)
gl.Vertex(-1.0, -1.0, -1.0)
gl.Color( 0.0, 1.0, 0.0)
gl.Vertex(-1.0, -1.0, 1.0)
gl.End()
 
 
rtri = rtri + 1.0
 
scene.SwapBuffers()
 
Nếu (rtri % 360 == 0) thì
nRound = nRound + 1
Cuối nếu
 
Nếu (nRound == ROUNDS) thì
t2 = os.clock()
print ("Number of rounds : ", ROUNDS)
print ("Elapsed time : ", (t2-t1)," seconds")
os.exit(1)
Cuối nếu
Cuối hàm
 
4.2.1.3.Nhóm tính toán với khối lượng lớn:
 
Bài toán 6: Bài toán đếm số lượng số nguyên tố nhỏ hơn hay bằng N (N là số nguyên khá lớn)
 
Mô tả:
oCho số nguyên dương N (10.000 hoặc 100.000).
oĐếm số lượng các số nguyên tố nhỏ hơn hay bằng N.
 
Thuật toán:
 
Int DemSoLuongSoNguyenTo(n)
{
MIN_DUONG = 1
SoLuongSNT = 0
Lặp i từ MIN_DUONG đến n làm
Nếu (i là số nguyên tố) thì
SoLuongSNT = SoLuongSNT + 1
Cuối nếu
Cuối lặp
Trả về SoLuongSNT
}
 
4.2.1.4.Loại ứng dụng Client/Server:
 
Bài toán 7: Bài toán Ping (Ping có echo, 1 client - 1 server).
Mô tả:
oXử lý tuần tự cho 1 client.
o1000 lần ping có data (với các data có kich thước khác nhau)
oĐo thời gian nhận và gởi data.
oTính trung bình cho 1000 lần.
 
Thuật toán:
 
Hầu hết, các thư viện của LUA và Python đều sử dụng lại thư viện có sẳn như: SDL, OPENGL nên sự khác nhau về hiệu năng giữa các chương trình của LUA và Python không đáng kể. Nên luận văn sẽ không minh họa bài toán Ping.
 
4.2.2.Cài đặt
 
Xem source code phần phụ lục.
 
4.3.Đánh giá hiệu năng
 
Tất cả các demo trong luận văn đều được khuyếch đại để tăng tính ngẫu nhiên và làm giảm độ ảnh hưởng của môi trường.
 
 
Lua
Python
Ruby
Nhận xét
Bài toán 1: Bài toán Fibonancy.
Tính F(30)
 
0,90 (giây)
1,78 (giây)
6,80 (giây)
LUA nhanh nhất
Bài toán 2: Bài toán sắp xếp nhị phân đệ quy (QuickSort).
Sắp xếp mảng random 10,000 số nguyên
 
2,67 (giây)
1,43 (giây)
5,59 (giây)
PYTHON nhanh nhất, nhưng LUA nhanh hơn Ruby rất nhiều.
Bài toán 3: Bài toán Image Morphing
6,452 (giây)
6,85 (giây)
 
LUA nhanh nhất
Bài toán 4: Bài toán quả bóng lăn(2D-SDL).
9,73 (giây)
9,75 (giây)
 
LUA nhanh hơn
Bài toán 5: Bài toán kim tự tháp xoay (3D). – 20 vòng
26,469 (giây)
32,16 (giây)
 
 
Bài toán 6: Đếm số lượng số nguyên tố nhỏ hơn hay bằng N (N là số nguyên khá lớn)
Nhập N = 10,000
 
7,91 (giây)
13,78 (giây)
56,06 (giây)
LUA nhanh nhất
Bài toán 7: Bài toán Ping (Ping có echo, 1 client - 1 server).
