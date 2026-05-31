# Windows-Fundamentals-2

task 1 

module này tiếp tục windows fundamentals 1

nội dung chính -> học thêm các công cụ có sẵn trong windows như: system configuration, uac settings, computer management, system information, resource monitor, command prompt, registry editor

để làm lab -> bấm start machine

task 2

ở task này, em học về system configuration và advanced system settings

system configuration còn được gọi là msconfig

msconfig là công cụ dùng để troubleshoot các lỗi liên quan đến quá trình khởi động windows

nói dễ hiểu hơn thì khi windows boot lỗi, service bị lỗi, hoặc nghi có thứ gì đó làm máy khởi động bất thường thì có thể dùng msconfig để kiểm tra

cách mở msconfig

```text
win + r -> msconfig -> enter
```

hoặc

```text
start menu -> search system configuration
```

lưu ý là muốn mở msconfig thì cần quyền local administrator

trong msconfig có 5 tab chính

```text
general
boot
services
startup
tools
```

tab general dùng để chọn cách windows load khi khởi động

normal startup -> khởi động bình thường, load đầy đủ driver và service

diagnostic startup -> chỉ load driver và service cơ bản, dùng để kiểm tra lỗi

selective startup -> cho phép chọn thành phần nào sẽ được load khi boot

tab boot dùng để chỉnh các tùy chọn khởi động của hệ điều hành

ví dụ có thể chỉnh safe boot, boot log hoặc timeout

trong forensics, tab boot có thể giúp kiểm tra máy có bị chỉnh option khởi động bất thường không

tab services liệt kê các service có trên hệ thống

service là dạng chương trình chạy nền trong windows

service có thể đang running hoặc stopped

trong forensics, tab services rất quan trọng vì malware có thể tạo service để tự chạy lại sau khi restart máy

nếu thấy service lạ, manufacturer lạ hoặc service nằm ở đường dẫn bất thường thì cần kiểm tra kỹ hơn

tab startup dùng để xem các chương trình tự chạy khi user đăng nhập

nhưng trong máy lab này là windows server nên tab startup thường không hiện giống windows 10 hoặc windows 11

với windows server, để xem startup user-level thì dùng lệnh

```text
win + r -> shell:startup
```

folder startup sẽ hiện các shortcut hoặc file được cấu hình chạy tự động khi user đăng nhập

trong forensics, startup folder cũng là nơi cần soi vì malware có thể đặt shortcut ở đây để tự chạy mỗi lần user login

tab tools chứa nhiều công cụ hệ thống có sẵn trong windows

mỗi tool sẽ có phần mô tả ngắn để biết công cụ đó dùng làm gì

khi chọn một tool, phần selected command sẽ hiện lệnh dùng để mở tool đó

có thể bấm launch để chạy tool hoặc copy command đem chạy bằng run / cmd

advanced system settings là nơi chỉnh các thiết lập nâng cao của hệ thống

cách mở

```text
start menu -> search view advanced system settings
```

trong advanced system settings có các mục quan trọng như performance và startup and recovery

performance dùng để chỉnh các thiết lập liên quan đến hiệu năng của windows

trong performance có phần page file

page file là bộ nhớ ảo mà windows dùng thêm khi ram bị đầy

khi ram không đủ, windows có thể dùng một phần ổ đĩa làm virtual memory để tránh chương trình bị crash

page file có thể cho biết các thông tin như

```text
ổ đĩa chứa page file
initial size
maximum size
windows có tự quản lý size không
```

trong forensics, page file có thể hữu ích vì đôi khi nó còn chứa dấu vết dữ liệu từng nằm trong ram

ví dụ có thể còn sót chuỗi text, command, đường dẫn file, hoặc dữ liệu liên quan đến process từng chạy

startup and recovery dùng để chỉnh hành vi của windows khi hệ thống bị lỗi nặng

ví dụ khi máy bị blue screen of death

windows có thể tạo crash dump để lưu lại thông tin tại thời điểm hệ thống bị crash

crash dump giúp admin hoặc analyst phân tích nguyên nhân lỗi

các loại crash dump thường gặp gồm

```text
automatic memory dump
kernel memory dump
small memory dump
complete memory dump
none
```

trong forensics, crash dump có thể chứa thông tin về process, driver hoặc lỗi hệ thống tại thời điểm crash

nếu máy bị malware làm crash hoặc driver độc hại gây lỗi thì crash dump có thể giúp tìm manh mối

tóm tắt task 2

msconfig -> dùng để troubleshoot lỗi startup

general -> chọn kiểu windows khởi động

boot -> chỉnh tùy chọn boot

services -> soi service chạy nền

startup -> soi app tự chạy khi login

tools -> xem command mở các công cụ windows

advanced system settings -> xem performance, page file và crash dump

trong forensics, task này giúp em kiểm tra service lạ, startup bất thường, bộ nhớ ảo và crash dump để tìm dấu hiệu hệ thống bị can thiệp

trả lời câu hỏi

```text
câu hỏi 1

what is the name of the service that lists systems internals as the manufacturer?

cách tìm

mở msconfig -> tab services -> tìm cột manufacturer có systems internals -> lấy tên service ở cột service
```

<img width="1905" height="1023" alt="image" src="https://github.com/user-attachments/assets/f7b4badb-0f15-479b-bd42-d7fc4a223a35" />

đáp án

```
psshutdown
```

```text
câu hỏi 2

whom is the windows license registered to?

cách tìm

mở msconfig -> tab tools -> chọn about windows -> bấm launch -> xem dòng registered to

đáp án

windows user
```

```text
câu hỏi 3

what is the command for windows troubleshooting?

cách tìm

mở msconfig -> tab tools -> chọn windows troubleshooting -> nhìn phần selected command

đáp án

c:\windows\system32\control.exe /name microsoft.troubleshooting
```

```text
câu hỏi 4

what command will open the control panel?

cách tìm

mở msconfig -> tab tools -> chọn control panel -> nhìn phần selected command

lab chỉ lấy tên file .exe, không lấy full path

đáp án

control.exe
```

