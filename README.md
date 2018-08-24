# SPC

SPC - Security Policy System.

That is my thesis, what i do when i am a intern.

Hệ thống quản lý chính sách an ninh, an toàn thông tin cho doanh nghiệp
1. Đặt vấn đề
- Hầu hết các máy tính đều được kết nối vào mạng internet, nơi mà đang
ngày càng trở nên không an toàn: bị cài đặt lén các phần mềm theo dõi
khi kết nối mạng không an toàn hoặc sử dụng các phần mềm không rõ
nguồn gốc.
- Mỗi doanh nghiệp, nhất là các doanh nghiệp trong lĩnh vực CNTT đều
cần xây dựng chính sách an ninh thông tin theo các quy định được ban
hành trong doanh nghiệp, nhằm đảm bảo an ninh, an toàn thông tin. Ví
dụ: kiểm soát việc cài đặt sử dụng phần mềm, sử dụng các thiết bị nhớ
ngoài, firewall, kiểm soát thời gian share các thư mục, dung lượng dữ
liệu trao đổi, ...
2. Tổ chức và hoạt động của hệ thống
Hoạt động theo mô hình Client/Server bao gồm các thành phần sau:
- Client: đảm nhận cập nhật dữ liệu từ server về máy người dùng, kiểm tra
các vi phạm phần mềm cài đặt, phần mềm chưa cài đặt, chính sách sử
dụng các thiết bị trên máy người dùng, thông báo cho người dùng biết
các phần mềm, thiết bị vi phạm chính sách sử dụng, hạn chế, kiểm soát
việc sử dụng các phần mềm, thiết bị, tiến trình theo chính sách đã được
cấu hình.
- Server: truy vấn, cập nhật, thêm mới, xóa người sử dụng, thông tin chính
sách sử dụng phần mềm, nhóm phần mềm, phần mềm bắt buộc, các chính
sách về thiết bị của người dùng. Đọc thông tin các chính sách sử dụng
phần mềm, nhóm phần mềm, phần mềm bắt buộc sử dụng, ... gửi cho
client. Cập nhật các thông tin vi phạm phần mềm, thời gian kết nối gần
đây nhất, phiên bản của phần mềm, hệ điều hành đang sử dụng ... của
client.
- Web quản trị: thiết lập chính sách cho các đối tượng, các phòng ban,
account, thống kê, quản lý danh sách người dùng và người quản lý.
3. Xây dựng hệ thống
Xây dựng hệ thống gồm 5 module:

- Module Server: gửi danh sách phân quyền chính sách về cho client, cập
nhật các chính sách vi phạm của client vào cơ sở dữ liệu.
- Module Service: nhận danh sách phân quyền chính sách từ Server, gửi
lên server các chính sách vi phạm của client, thiết lập lại các chính sách
an ninh quan trọng
- Module GUI: hiển thị và thông báo khi có chính sách vi phạm
- Module Update: tải các bản cập nhật mới nhất, bật lại module service khi
có vấn đề xảy ra.
- Module Quản trị: xây dựng trang web cho quản trị viên dễ dàng thao tác
phân quyền cho người dùng.
4. Các chức năng xây dựng trên hệ thống
- Kiểm tra vi phạm phần mềm.
- Thiết lập các thiết bị: sử dụng usb, khóa màn hình, thời gian share thư
mục.
- Thiết lập chính sách an ninh của hệ điều hành: bật lại firewall nếu bị off,
thiết lập các thuộc tính mật khẩu người dùng.
- Tiến hành phân quyền phần mềm, thiết lập các chính sách, thiết bị qua
web quản trị.
5. Các đối tượng
- Các phần mềm máy tính
- Các nhóm phần mềm
- Các thiết bị gắn với máy tính người sử dụng.
- Người sử dụng, được thể hiện qua các account. Trên account là các
phòng ban được xây dựng theo sơ đồ hình cây.
6. Nguyên tắc kiểm soát các đối tượng
- Các node con thừa kế các đối tượng và chính sách đã được thiết lập cho
node cha.
- Khi thay đổi chính sách cho đối tượng ở node con thì chính sách được
thiết lập lại (ghi đè lên chính sách cũ).
- Quan hệ giữa người sử dụng với các đối tượng khác qua chính sách:
+ Phải: bắt buộc cài đặt, sử dụng, nếu NSD sẽ bị cảnh báo nếu không cài
đặt/sử dụng đối tượng.
+ Cấm: không được phép cài đặt, sử dụng. NSD sẽ bị cảnh báo nếu vi
phạm cài đặt/sử dụng.

+ Không xác định: được phép cài đặt, sử dụng. NSD sẽ không bị cảnh
báo nếu cài hoặc ko cài phần mềm.
Hệ thống kiểm soát các đối tượng như sau:
o Khi kiểm tra vi phạm, hệ thống đối chiếu danh sách phần mềm cài
đặt trên máy NSD với danh sách các phần mềm đã được thiết lập
chính sách trong danh sách của NSD. Các trường hợp sau bị coi là
vi phạm:
 NSD cài đặt phần mềm được thiết lập là Không được cài
(Cấm)
 NSD không cài đặt phần mềm đã được thiết lập là Phải cài
(Phải)
 NSD cài đặt phần mềm ngoài danh sách phần mềm đã được
thiết lập chính sách của NSD.

o Khi so sánh phần mềm cài đặt trên máy tính NSD, phần mềm trên
danh sách phần mềm của hệ thống thì sử dụng phép so sánh bằng
(tên phần mềm giống hệt nhau).
o Thiết bị. Khi kiểm tra vi phạm, hệ thống rà soát lại trên danh sách
(database) thiết bị được thiết lập chính sách của NSD, và kiểm tra
trạng thái sử dụng các thiết bị trên máy NSD. Các trường hợp sau
bị coi là vi phạm: sử dụng các thiết bị được thiết lập chính sách là
Không được sử dụng(Cấm); NSD không sử dụng thiết bị đã được
thiết lập chính sách là Phải sử dụng(Phải).


1. Thiết kế ban đầu: 
* Cơ sở dữ liệu:
	- Server: MYSQL
	- Client: SQLite
* Server - Client: socket - C++ - Qt ( để ko phụ thuộc hệ điều hành )
* GUI:
	- Client: QT desktop - C++
	- Server: Web quản trị của admin - ASP.NET MVC - C#
