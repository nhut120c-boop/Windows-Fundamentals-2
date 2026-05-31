# Windows-Fundamentals-2

task 1 

module này tiếp tục windows fundamentals 1

nội dung chính -> học thêm các công cụ có sẵn trong windows như: system configuration, uac settings, computer management, system information, resource monitor, command prompt, registry editor

để làm lab -> bấm start machine

task 2

task 2

ở task này, em học về system configuration và advanced system settings

system configuration còn gọi là msconfig

msconfig -> công cụ dùng để troubleshoot lỗi khởi động windows

nó thường dùng khi máy boot lỗi, service lỗi, hoặc cần kiểm tra thành phần nào đang ảnh hưởng lúc windows khởi động

cách mở msconfig

```text
win + r -> msconfig -> enter
```

hoặc

```text
start menu -> search system configuration
```

lưu ý: muốn mở msconfig thì cần quyền local administrator

msconfig có 5 tab chính

```text
general
boot
services
startup
tools
```

tab general

tab này dùng để chọn kiểu windows load khi khởi động

normal startup -> khởi động bình thường, load đầy đủ driver và service

diagnostic startup -> chỉ load driver và service cơ bản, dùng để test lỗi

selective startup -> cho chọn phần nào sẽ được load khi boot

tab boot

tab này dùng để chỉnh các tùy chọn boot của hệ điều hành

ví dụ: safe boot, boot log, timeout

trong forensics, tab này có thể giúp kiểm tra máy có bị chỉnh boot option bất thường không

tab services

tab này liệt kê các service trên hệ thống

service -> app chạy nền trong windows

service có thể đang running hoặc stopped

trong forensics, tab services rất đáng soi vì malware có thể tạo service để tự chạy lại sau khi restart máy

```text
câu hỏi 1

what is the name of the service that lists systems internals as the manufacturer?

cách tìm

mở msconfig -> services -> nhìn cột manufacturer -> tìm dòng có systems internals -> lấy tên service ở cột service

=> đáp án

lấy trực tiếp trong máy lab
```

tab startup

tab này dùng để xem startup item

nhưng trong máy lab là windows server nên tab startup thường không hiện gì hữu ích như windows 10/11

muốn xem startup user-level thì dùng

```text
win + r -> shell:startup
```

folder này sẽ hiện các shortcut hoặc file được cấu hình chạy tự động khi user đăng nhập

trong forensics, startup folder là chỗ cần kiểm tra vì malware có thể đặt shortcut ở đây để tự chạy khi login

tab tools

tab này chứa nhiều công cụ hệ thống có sẵn trong windows

khi chọn một tool, phần selected command sẽ hiện lệnh dùng để mở tool đó

có thể bấm launch để chạy tool hoặc copy command đem chạy bằng run / cmd

```text
câu hỏi 2

whom is the windows license registered to?

cách tìm

mở msconfig -> tools -> chọn about windows -> bấm launch -> xem dòng registered to

=> đáp án

lấy tên hiển thị trong cửa sổ about windows
```

```text
câu hỏi 3

what is the command for windows troubleshooting?

cách tìm

mở msconfig -> tools -> chọn windows troubleshooting -> nhìn phần selected command

=> đáp án

copy đúng command hiện trong selected command
```

```text
câu hỏi 4

what command will open the control panel?

cách tìm

mở msconfig -> tools -> chọn control panel -> nhìn phần selected command

lưu ý

lab chỉ hỏi tên file .exe, không lấy full path

=> đáp án

control.exe
```

advanced system settings

advanced system settings -> nơi chỉnh các thiết lập nâng cao của hệ thống

cách mở

```text
start menu -> search view advanced system settings
```

trong phần advanced có 2 mục quan trọng là performance và startup and recovery

performance

performance settings -> dùng để chỉnh hiệu năng của windows

trong đó có page file

page file -> bộ nhớ ảo windows dùng thêm khi ram đầy

khi ram không đủ, windows có thể dùng một phần ổ đĩa làm virtual memory để tránh app bị crash

page file cho biết các thông tin như

```text
ổ đĩa chứa page file
initial size
maximum size
windows có tự quản lý size không
```

trong forensics, page file có thể chứa dấu vết dữ liệu từng nằm trong ram

startup and recovery

startup and recovery -> dùng để chỉnh hành vi khi windows lỗi nặng

ví dụ khi máy bị blue screen of death

windows có thể tạo crash dump để lưu thông tin tại thời điểm hệ thống crash

crash dump giúp admin hoặc analyst phân tích nguyên nhân lỗi

các loại crash dump thường gặp

```text
automatic memory dump
kernel memory dump
small memory dump
complete memory dump
none
```

trong forensics, crash dump có thể chứa thông tin tiến trình, driver hoặc lỗi hệ thống tại thời điểm crash

=> có thể dùng để tìm nguyên nhân máy bị lỗi hoặc bị malware làm crash

tóm tắt task 2

msconfig -> troubleshoot startup

services -> soi service chạy nền

startup -> soi app tự chạy khi đăng nhập

tools -> xem command mở các công cụ windows

advanced system settings -> xem page file và crash dump

trong forensics, task này giúp em kiểm tra service lạ, startup bất thường, bộ nhớ ảo và crash dump để tìm dấu hiệu hệ thống bị can thiệp
