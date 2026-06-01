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
```
<img width="1894" height="1030" alt="image" src="https://github.com/user-attachments/assets/0ad0b364-795e-4cde-803c-9319667f566d" />

đáp án

```
windows user
```


```text
câu hỏi 3

what is the command for windows troubleshooting?

cách tìm

mở msconfig -> tab tools -> chọn windows troubleshooting -> nhìn phần selected command

```
<img width="1903" height="1028" alt="image" src="https://github.com/user-attachments/assets/0d97a21b-59fd-4e97-ae1a-a1b6a6815d41" />

đáp án
```
c:\windows\system32\control.exe /name microsoft.troubleshooting
```

```text
câu hỏi 4

what command will open the control panel?

cách tìm

mở msconfig -> tab tools -> chọn system properties -> nhìn phần selected command
```

<img width="1910" height="1012" alt="image" src="https://github.com/user-attachments/assets/eb53da1f-5b9d-42f3-955c-ae82abbefb7e" />

đáp án

```
control.exe
```

task 3

ở task này, em học về cách thay đổi uac settings trong windows

uac là user account control

uac dùng để cảnh báo khi app hoặc user muốn thay đổi những thứ ở cấp hệ thống

ví dụ như cài phần mềm, sửa setting quan trọng, hoặc chạy chương trình cần quyền admin

nói dễ hiểu hơn

uac giống như lớp hỏi lại của windows

nó không cho app tự nhiên chạy quyền cao ngay lập tức

nếu chương trình cần quyền admin -> windows sẽ hiện bảng xác nhận

mục đích của uac là giảm rủi ro malware tự ý sửa hệ thống

trong task này, uac settings có thể mở thông qua system configuration -> tools

trong cửa sổ uac settings sẽ có một thanh trượt

thanh trượt này có 4 mức bảo mật

mức 1

always notify

đây là mức cao nhất

windows sẽ báo mỗi khi app hoặc chính user muốn thay đổi hệ thống

màn hình sẽ bị làm tối lại bằng secure desktop

mức này an toàn hơn nhưng có thể hơi phiền vì hỏi nhiều

mức 2

notify for apps

windows chỉ báo khi app cố thay đổi hệ thống

nếu user tự đổi setting windows thì thường không báo

đây là mức mặc định của windows

mức này cân bằng giữa bảo mật và tiện dụng

mức 3

notify without dimming

giống mức notify for apps

nhưng màn hình không bị làm tối

mức này kém an toàn hơn một chút vì không dùng secure desktop

mức 4

never notify

windows sẽ không cảnh báo khi app hoặc user thay đổi hệ thống

mức này không được khuyến nghị

vì nếu malware chạy được thì nó có thể dễ dàng thay đổi hệ thống hơn mà user không được cảnh báo

trong forensics, uac settings cũng đáng chú ý

nếu thấy uac bị tắt hoặc đặt ở never notify -> có thể là dấu hiệu máy bị cấu hình yếu bảo mật hoặc đã bị malware chỉnh để dễ leo quyền / chạy lệnh nguy hiểm

vì vậy khi điều tra máy windows, em có thể kiểm tra uac để biết hệ thống có đang bật lớp cảnh báo quyền admin hay không

trả lời câu hỏi

```text
câu hỏi

what is the command to open user account control settings?

câu này hỏi file .exe dùng để mở cửa sổ user account control settings

đề nói chỉ lấy tên file .exe, không lấy full path

vì vậy không cần ghi đường dẫn đầy đủ

```
<img width="1919" height="977" alt="image" src="https://github.com/user-attachments/assets/07401c87-46d2-41cf-b67e-b83bcc7dc350" />

đáp án

```
UserAccountControlSettings.exe
```

task 4

ở task này, em học về computer management trên windows

computer management là công cụ gom nhiều tiện ích quản lý hệ thống vào một cửa sổ

thay vì mở từng tool riêng lẻ, em có thể dùng computer management để xem nhiều phần quan trọng như task scheduler, event viewer, shared folders, local users and groups, performance, device manager, disk management và services

computer management có 3 nhóm chính

```text
system tools
storage
services and applications
```

system tools là nhóm dùng để xem và quản lý các thành phần hệ thống

trong system tools có task scheduler

task scheduler dùng để tạo và quản lý các tác vụ tự động

một task có thể chạy chương trình, script hoặc command theo điều kiện nhất định

ví dụ task có thể chạy khi user đăng nhập, khi máy khởi động, hoặc theo lịch cố định mỗi ngày

trong forensics, task scheduler rất quan trọng

vì malware có thể tạo scheduled task để tự chạy lại sau khi restart hoặc sau khi user login

khi soi task scheduler, em cần chú ý các phần như

```text
tên task
trạng thái task
trigger
last run time
last run result
actions
command được chạy
```

trigger cho biết task chạy khi nào

actions cho biết task sẽ chạy chương trình hoặc command gì

nếu thấy action chạy powershell, cmd, file exe lạ hoặc script trong thư mục lạ thì cần điều tra kỹ hơn

trong ảnh lab, task scheduler library hiển thị các task có sẵn trên máy

task npcapwatchdog được hỏi trong lab vì nó là scheduled task có cấu hình thời điểm chạy cụ thể

muốn biết task chạy lúc nào thì phải xem cột triggers

event viewer là công cụ dùng để xem log sự kiện trên windows

event log giống như dấu vết hoạt động của hệ thống

nó ghi lại các sự kiện như lỗi chương trình, đăng nhập thành công, đăng nhập thất bại, service lỗi, driver lỗi hoặc hoạt động bảo mật

event viewer có 3 phần chính

```text
khung trái -> cây thư mục log
khung giữa -> danh sách / nội dung event
khung phải -> actions
```

các loại event thường gặp gồm

```text
error
warning
information
success audit
failure audit
```

error -> lỗi nghiêm trọng

warning -> cảnh báo, có thể chưa lỗi ngay nhưng có nguy cơ

information -> thông tin hoạt động bình thường

success audit -> hành động bảo mật thành công, ví dụ đăng nhập thành công

failure audit -> hành động bảo mật thất bại, ví dụ đăng nhập sai

trong windows logs có các log phổ biến như

```text
application
security
system
```

application -> log của ứng dụng

security -> log đăng nhập, audit, truy cập tài nguyên

system -> log của thành phần hệ thống, driver, service

trong forensics, event viewer giúp em dựng lại timeline và biết chuyện gì đã xảy ra trên máy

ví dụ có thể soi đăng nhập bất thường, service bị lỗi, task được chạy, hoặc phần mềm nào gây lỗi

shared folders dùng để xem các thư mục đang được chia sẻ trên máy

trong shared folders có các mục như shares, sessions và open files

shares -> danh sách thư mục đang share

sessions -> user nào đang kết nối tới share

open files -> file nào đang được user khác mở qua share

trong windows có các share mặc định như

```text
admin$
c$
ipc$
```

dấu $ phía sau tên share nghĩa là hidden share

hidden share không hiện bình thường khi duyệt mạng, nhưng vẫn có thể truy cập nếu biết đúng đường dẫn và có quyền

trong forensics, shared folders giúp kiểm tra máy có đang share thư mục nhạy cảm hay không

nếu có folder lạ được share, nhất là hidden share, thì cần xem permissions để biết ai có quyền truy cập

local users and groups là phần quản lý user và group local

phần này giống lusrmgr.msc đã học ở windows fundamentals 1

nó giúp xem user nào tồn tại trên máy và user đó thuộc group nào

trong forensics, phần này giúp kiểm tra user lạ, user mới tạo hoặc user bị thêm vào administrators

performance có performance monitor

performance monitor dùng để xem dữ liệu hiệu năng của hệ thống theo thời gian thực hoặc từ log file

nó giúp kiểm tra cpu, ram, disk, network và các counter khác

trong forensics hoặc troubleshooting, nếu máy chậm bất thường thì perfmon có thể giúp xác định tiến trình hoặc tài nguyên nào có vấn đề

device manager dùng để xem và cấu hình phần cứng trên máy

ví dụ như disk drives, display adapters, network adapters, processors, keyboards, mice và system devices

trong forensics, device manager có thể giúp kiểm tra thiết bị lạ, driver lạ hoặc network adapter bất thường

storage là nhóm liên quan đến lưu trữ

trong task này, phần quan trọng là disk management

disk management dùng để xem và quản lý ổ đĩa, partition và drive letter

có thể dùng để tạo ổ mới, extend partition, shrink partition hoặc đổi drive letter

trong ảnh lab, disk management hiển thị ổ c: và system reserved

trong forensics, disk management giúp kiểm tra máy có bao nhiêu ổ, partition nào đang tồn tại, file system là gì và có vùng nào bất thường không

services and applications là nhóm chứa services và wmi control

services dùng để xem toàn bộ service trên máy

service là chương trình chạy nền trong windows

mỗi service có display name, service name, status, startup type và path to executable

display name là tên hiển thị dễ đọc

service name là tên thật hệ thống dùng để quản lý service

path to executable cho biết file nào được chạy khi service start

startup type cho biết service khởi động như thế nào

```text
automatic -> tự chạy khi boot
manual -> chỉ chạy khi được gọi
disabled -> không cho chạy
```

trong forensics, services là nơi rất cần soi

vì malware hay tạo service mới để persistence

nếu service có path lạ, tên lạ, chạy từ temp/appdata/downloads hoặc startup type là automatic thì cần kiểm tra kỹ hơn

wmi control dùng để cấu hình windows management instrumentation

wmi cho phép quản lý windows bằng script hoặc powershell, cả local và remote

trong forensics, wmi cũng đáng chú ý vì attacker có thể lợi dụng wmi để chạy lệnh hoặc tạo persistence

tóm tắt task 4

computer management -> công cụ gom nhiều phần quản lý windows

task scheduler -> soi task tự động chạy

event viewer -> soi log sự kiện

shared folders -> soi thư mục đang share

local users and groups -> soi user và group

performance -> soi hiệu năng hệ thống

device manager -> soi phần cứng và driver

disk management -> soi ổ đĩa và partition

services -> soi service chạy nền

wmi control -> quản lý wmi

trong forensics, task này quan trọng vì nó gom nhiều nơi có thể để lại dấu vết tấn công, đặc biệt là scheduled task, event log, hidden share, service lạ và disk/partition bất thường

trả lời câu hỏi

```text
câu hỏi 1

what is the command to open computer management

câu này hỏi file .msc dùng để mở computer management

vì computer management là microsoft management console nên nó được mở bằng một file .msc

đề nói chỉ lấy tên file .msc, không lấy full path

đáp án

compmgmt.msc
```

```text
câu hỏi 2

when is the npcapwatchdog scheduled task set to run at

câu này hỏi task npcapwatchdog được đặt chạy khi nào

muốn biết thời điểm task chạy thì phải vào task scheduler library và xem cột triggers

trigger là điều kiện kích hoạt task

trong lab, npcapwatchdog có trigger là chạy lúc hệ thống khởi động

đáp án

at system startup
```

```text
câu hỏi 3

what is the name of the hidden folder that is shared

câu này hỏi tên folder bị share dạng hidden

trong windows, share có dấu $ ở cuối thường là hidden share

muốn tìm thì vào computer management -> shared folders -> shares

ở đó sẽ thấy danh sách các thư mục đang được chia sẻ

folder hidden share trong lab có tên là

đáp án

sh4r3dF0ld3r
```

