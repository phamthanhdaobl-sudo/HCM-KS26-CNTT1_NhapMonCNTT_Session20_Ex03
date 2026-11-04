# HCM-KS26-CNTT1_NhapMonCNTT_Session20_Ex03
BÀI 3 – SESSION 20: QUẢN LÝ RỦI RO KHI MẤT THIẾT BỊ XÁC THỰC

Họ và tên: Phạm Thành Đạo
Lớp: HCM-KS26-CNTT1
Môn học: An toàn thông tin

1. Phân tích tình huống

1.1. Bối cảnh

Tôi là Lead Developer của một dự án và đang sử dụng Google Authenticator trên điện thoại để tạo mã xác thực hai yếu tố (2FA) khi đăng nhập vào tài khoản AWS.

Tuy nhiên, tôi vừa bị mất điện thoại. Đây cũng là thiết bị duy nhất chứa mã Google Authenticator dùng để xác thực tài khoản AWS.

Khi đăng nhập, hệ thống yêu cầu nhập mã OTP nhưng tôi không thể lấy được mã xác thực do không còn thiết bị.

Các rủi ro có thể xảy ra:

1. Không thể đăng nhập AWS để bảo trì và quản lý hệ thống.
2. Kẻ nhặt được điện thoại có thể tìm cách truy cập thông tin cá nhân hoặc tài khoản nếu thiết bị không được bảo vệ tốt.
3. Nếu kẻ xấu có cả mật khẩu tài khoản và quyền truy cập thiết bị xác thực, nguy cơ chiếm đoạt tài khoản sẽ tăng cao.
4. Hệ thống dự án có thể bị gián đoạn nếu không có phương án khôi phục quyền truy cập.

1.2. Mục tiêu xử lý

* Khôi phục quyền truy cập AWS bằng phương thức xác thực dự phòng hợp lệ.
* Vô hiệu hóa thiết bị MFA đã mất.
* Ngăn chặn người nhặt được điện thoại sử dụng thông tin xác thực.
* Thiết lập thiết bị xác thực mới và cấp mã dự phòng mới.
* Đảm bảo hoạt động của hệ thống không bị gián đoạn.

2. Thiết kế quy trình sử dụng Backup Codes

2.1. Backup Codes là gì?

Backup Codes (Mã khôi phục hoặc mã dự phòng) là những mã xác thực được hệ thống cấp trước để người dùng sử dụng khi không thể truy cập thiết bị MFA chính.

Đặc điểm:

* Được tạo và cấp trước khi xảy ra sự cố.
* Có thể sử dụng để khôi phục quyền truy cập khi mất thiết bị xác thực.
* Mỗi mã thường chỉ được sử dụng một lần.
* Sau khi sử dụng, mã đó sẽ không còn hiệu lực.
* Cần được lưu trữ tại nơi an toàn, độc lập với thiết bị xác thực chính.

Lưu ý: Backup Codes không phải mã OTP được Google Authenticator tự động tạo ra. Đây là các mã khôi phục do dịch vụ hỗ trợ MFA cấp.

2.2. Quy trình khôi phục quyền truy cập

Bước 1: Báo mất thiết bị và bảo vệ điện thoại.

* Sử dụng tính năng Find My Device hoặc Find My iPhone để định vị điện thoại nếu có thể.
* Khóa thiết bị từ xa để ngăn người khác truy cập.
* Nếu xác định không thể lấy lại thiết bị, thực hiện xóa dữ liệu từ xa khi cần thiết.
* Thông báo cho bộ phận IT hoặc người quản trị dự án.
* Không đăng nhập tài khoản quan trọng trên thiết bị không đáng tin cậy.

Bước 2: Sử dụng Backup Codes để xác thực.

* Truy cập trang đăng nhập AWS bằng địa chỉ chính thức.
* Nhập thông tin tài khoản và mật khẩu.
* Khi hệ thống yêu cầu MFA, chọn phương thức xác thực dự phòng nếu dịch vụ hỗ trợ.
* Nhập một Backup Code chưa sử dụng.
* Hoàn tất quá trình xác thực và đăng nhập.

Bước 3: Hủy thiết bị MFA cũ.

Sau khi khôi phục quyền truy cập:

* Truy cập phần quản lý bảo mật hoặc Security Credentials.
* Xác định thiết bị MFA đã mất.
* Vô hiệu hóa hoặc gỡ liên kết thiết bị MFA cũ.
* Thu hồi các phiên đăng nhập và thông tin xác thực có nguy cơ bị lộ.
* Đổi mật khẩu tài khoản nếu có khả năng điện thoại bị truy cập trái phép.

Bước 4: Thiết lập thiết bị MFA mới.

* Cài đặt Google Authenticator trên điện thoại mới hoặc thiết bị đáng tin cậy.
* Truy cập phần thiết lập MFA của AWS.
* Đăng ký thiết bị xác thực mới bằng mã QR hoặc khóa thiết lập.
* Nhập mã OTP để hoàn tất xác minh.
* Kiểm tra khả năng đăng nhập bằng thiết bị MFA mới.

Bước 5: Cấp và lưu trữ Backup Codes mới.

* Tạo bộ mã khôi phục mới nếu dịch vụ hỗ trợ.
* Kiểm tra mã mới đã hoạt động.
* Đảm bảo các mã đã sử dụng hoặc bộ mã cũ không còn hiệu lực theo cơ chế của dịch vụ.
* Lưu mã mới trong Password Manager được mã hóa hoặc bản giấy cất trong két bảo mật.
* Không lưu mã mới trong thư viện ảnh hoặc ghi chú không được bảo vệ trên điện thoại.

Kết luận: Quy trình khôi phục cần đảm bảo vừa lấy lại được quyền truy cập, vừa vô hiệu hóa thiết bị đã mất và thiết lập lại các phương thức xác thực an toàn.

3. Báo cáo phân tích theo mô hình IPO

IPO là mô hình mô tả quá trình hoạt động của một hệ thống thông qua ba thành phần:

* Input: Dữ liệu đầu vào.
* Process: Quá trình xử lý.
* Output: Kết quả đầu ra.

3.1. Input – Dữ liệu đầu vào

Các thông tin cần thiết để khôi phục quyền truy cập:

Thành phần	Mô tả
Tài khoản AWS	Tài khoản cần khôi phục quyền truy cập
Mật khẩu tài khoản	Thông tin xác thực chính của người dùng
Backup Codes	Mã dự phòng hợp lệ, chưa sử dụng
Thiết bị mới	Điện thoại hoặc thiết bị đáng tin cậy để thiết lập MFA
Thông tin liên hệ	Email và số điện thoại khôi phục đã đăng ký

Yêu cầu bảo mật:

* Backup Codes phải được lấy từ nơi lưu trữ an toàn.
* Không sử dụng mã đã hết hạn hoặc đã được sử dụng.
* Không gửi mã dự phòng cho người khác.
* Không đưa mã thật vào mã nguồn hoặc repository GitHub.

3.2. Process – Quá trình xử lý

Quá trình xử lý gồm các bước:

Bước	Hoạt động	Mục đích
1	Khóa và bảo vệ điện thoại bị mất	Ngăn người khác truy cập thiết bị
2	Đăng nhập bằng mật khẩu và Backup Code	Xác thực người dùng hợp lệ
3	Vô hiệu hóa thiết bị MFA cũ	Ngăn thiết bị đã mất tiếp tục được sử dụng
4	Thu hồi phiên đăng nhập và kiểm tra hoạt động bất thường	Ngăn chặn truy cập trái phép
5	Thiết lập MFA trên thiết bị mới	Khôi phục khả năng xác thực
6	Cấp mã khôi phục mới và lưu trữ an toàn	Chuẩn bị cho sự cố tiếp theo

3.3. Output – Kết quả đầu ra

Sau khi hoàn thành quy trình, hệ thống cần đạt được các kết quả:

1. Lead Developer khôi phục được quyền truy cập vào tài khoản AWS.
2. Thiết bị MFA cũ đã bị vô hiệu hóa hoặc gỡ liên kết.
3. Điện thoại bị mất không còn được sử dụng để xác thực tài khoản.
4. Thiết bị mới đã được đăng ký MFA thành công.
5. Bộ Backup Codes mới được lưu trữ an toàn.
6. Mật khẩu và các phiên đăng nhập đã được kiểm tra, thay đổi hoặc thu hồi khi cần thiết.
7. Hệ thống AWS tiếp tục hoạt động bình thường và giảm nguy cơ truy cập trái phép.

Sơ đồ mô hình IPO:

+-----------------------------+
|           INPUT             |
|                             |
| - Tài khoản AWS             |
| - Mật khẩu                  |
| - Backup Codes              |
| - Thiết bị mới              |
| - Thông tin khôi phục       |
+-----------------------------+
              |
              v
+-----------------------------+
|          PROCESS            |
|                             |
| 1. Khóa điện thoại cũ       |
| 2. Xác thực bằng mã dự phòng|
| 3. Hủy MFA cũ               |
| 4. Thu hồi phiên đăng nhập  |
| 5. Thiết lập MFA mới        |
| 6. Cấp mã dự phòng mới      |
+-----------------------------+
              |
              v
+-----------------------------+
|           OUTPUT            |
|                             |
| - Khôi phục quyền truy cập  |
| - Thiết bị cũ bị vô hiệu hóa|
| - MFA mới hoạt động         |
| - Backup Codes mới an toàn  |
| - Hệ thống được bảo vệ      |
+-----------------------------+

4. Giải thích tại sao không được lưu Backup Codes dưới dạng ảnh trong thư viện điện thoại

Việc lưu Backup Codes dưới dạng ảnh trong thư viện điện thoại là một hành động không an toàn, đặc biệt khi điện thoại chính là thiết bị có nguy cơ bị mất hoặc đánh cắp.

Lý do thứ nhất: Có thể bị truy cập trực tiếp khi mất điện thoại.

Nếu người nhặt được điện thoại mở khóa thành công, họ có thể truy cập thư viện ảnh và xem các mã khôi phục.

Lý do thứ hai: Ảnh có thể tự động đồng bộ lên Cloud.

Nhiều điện thoại có tính năng tự động đồng bộ ảnh lên iCloud, Google Photos hoặc các dịch vụ lưu trữ trực tuyến.

Nếu tài khoản Cloud bị xâm nhập, kẻ xấu có thể tìm thấy ảnh chứa Backup Codes.

Lý do thứ ba: Ảnh dễ bị sao chép và chia sẻ.

Hình ảnh có thể bị gửi qua tin nhắn, email hoặc ứng dụng mạng xã hội mà người dùng không nhận ra mức độ rủi ro.

Lý do thứ tư: Không có lớp bảo vệ chuyên biệt cho từng mã.

Ảnh thông thường không có cơ chế quản lý mã dự phòng, theo dõi mã đã sử dụng hoặc kiểm soát việc truy cập như một Password Manager chuyên dụng.

Giải pháp lưu trữ an toàn:

Nơi lưu trữ	Đánh giá
Password Manager có mã hóa	Nên sử dụng
Bản giấy cất trong két sắt	Nên sử dụng
Ảnh trong thư viện điện thoại	Không nên
Ảnh đồng bộ lên Cloud thông thường	Không nên
File TXT không mã hóa	Không nên
Email hoặc tin nhắn nhóm	Không nên
Repository GitHub công khai	Tuyệt đối không

Kết luận: Backup Codes cần được lưu ở một nơi an toàn và độc lập với điện thoại dùng để xác thực chính. Việc lưu bản giấy trong két hoặc sử dụng Password Manager được bảo vệ tốt sẽ giảm nguy cơ mất quyền kiểm soát tài khoản.

5. Giải pháp phòng ngừa khi mất thiết bị xác thực

Để tránh lặp lại tình huống tương tự, với vai trò Lead Developer, tôi đề xuất:

1. Thiết lập nhiều phương thức MFA.

* Đăng ký nhiều thiết bị MFA nếu dịch vụ hỗ trợ.
* Chuẩn bị một thiết bị xác thực dự phòng.
* Ưu tiên sử dụng Security Key hoặc Passkey khi phù hợp.

2. Lưu Backup Codes độc lập với điện thoại.

* Lưu trong Password Manager có mã hóa.
* Có thể in bản giấy và cất trong két bảo mật.
* Không lưu mã khôi phục trong thư viện ảnh hoặc email thông thường.

3. Bảo vệ điện thoại cá nhân.

* Sử dụng mật khẩu mở khóa mạnh.
* Bật Face ID hoặc Touch ID.
* Bật tính năng định vị và khóa thiết bị từ xa.
* Không chia sẻ mật khẩu mở khóa điện thoại.

4. Xây dựng quy trình khôi phục cho nhóm dự án.

* Phân quyền quản trị AWS rõ ràng.
* Có ít nhất một quản trị viên dự phòng được ủy quyền.
* Không chia sẻ chung tài khoản hoặc mã MFA giữa các thành viên.
* Kiểm tra định kỳ khả năng khôi phục quyền truy cập.

5. Kiểm tra định kỳ.

* Kiểm tra các thiết bị MFA đang được đăng ký.
* Kiểm tra mã khôi phục còn hiệu lực.
* Kiểm tra lịch sử đăng nhập.
* Thu hồi thiết bị hoặc phiên đăng nhập không còn sử dụng.

6. Lưu ý thực tế đối với tài khoản AWS

Trong thực tế, không phải mọi loại tài khoản AWS đều hỗ trợ Backup Codes theo cách giống GitHub.

Theo hướng dẫn AWS:

* Với IAM User, nếu mất thiết bị MFA và không có thiết bị MFA thay thế, người dùng cần liên hệ quản trị viên AWS để vô hiệu hóa MFA cũ và đăng ký thiết bị mới.
* Với Root User, AWS hỗ trợ quy trình xác minh danh tính thay thế thông qua email và số điện thoại đã đăng ký. Nếu không thể xác minh, cần liên hệ AWS Support.
* AWS khuyến nghị đăng ký nhiều thiết bị MFA để duy trì quyền truy cập khi một thiết bị bị mất.

Vì vậy, quy trình Backup Codes ở trên là quy trình nghiệp vụ áp dụng cho dịch vụ có hỗ trợ mã khôi phục. Khi triển khai thực tế trên AWS, cần sử dụng đúng cơ chế khôi phục tương ứng với loại tài khoản và cấu hình MFA.

Tài liệu tham khảo chính thức:

* AWS – Multi-factor authentication in IAM: https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa.html
* AWS – Recover an MFA protected identity: https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa_lost-or-broken.html

7. Triển khai và nộp bài trên GitHub

7.1. Tên repository

Theo định dạng đề bài:

[Tên Lớp]_[Tên Môn Học]_Session19_Ex03

Ví dụ:

HCM-KS26-CNTT1_ATTT_Session19_Ex03

Tên môn học có thể điều chỉnh theo tên chính xác trên Portal.

7.2. Cấu trúc repository đề xuất

HCM-KS26-CNTT1_ATTT_Session19_Ex03/
│
├── README.md
├── report.md
└── ipo-process.md

Chức năng các file:

* README.md: Giới thiệu bài tập và mục tiêu.
* report.md: Nội dung phân tích tình huống mất thiết bị xác thực.
* ipo-process.md: Mô tả quy trình khôi phục theo mô hình IPO.

7.3. Nội dung README.md mẫu

# Session 20 - Exercise 03
## Quản lý rủi ro khi mất thiết bị xác thực
### 1. Mục tiêu
- Hiểu vai trò của Backup Codes.
- Xây dựng quy trình khôi phục MFA.
- Bảo vệ tài khoản khi mất điện thoại.
- Phân tích mô hình Input - Process - Output.
### 2. Cấu trúc repository
- report.md: Báo cáo phân tích tình huống.
- ipo-process.md: Quy trình xử lý theo mô hình IPO.
### 3. Giải pháp
- Sử dụng Backup Codes khi dịch vụ hỗ trợ.
- Vô hiệu hóa thiết bị MFA đã mất.
- Đăng ký thiết bị MFA mới.
- Lưu mã dự phòng tại nơi an toàn.
### 4. Kết luận
Luôn chuẩn bị phương án khôi phục
trước khi xảy ra sự cố mất thiết bị.

7.4. Các bước đưa bài lên GitHub

1. Đăng nhập GitHub.
2. Chọn New repository.
3. Nhập tên repository theo đúng định dạng.
4. Chọn Public nếu giảng viên yêu cầu công khai.
5. Tạo repository.
6. Tải các file README.md, report.md và ipo-process.md lên GitHub.
7. Kiểm tra nội dung và cấu trúc repository trước khi nộp.

Nếu sử dụng Git trên máy tính, thực hiện:

git init
git add .
git commit -m "Complete Session 20 Exercise 03"
git branch -M main
git remote add origin https://github.com/USERNAME/REPOSITORY.git
git push -u origin main

Thay USERNAME và REPOSITORY bằng thông tin thực tế của tài khoản GitHub.

Lưu ý bảo mật: Không đưa Backup Codes thật, mật khẩu AWS, mã QR MFA hoặc Secret Key vào repository, kể cả khi repository ở chế độ Private.

7.5. Nộp bài trên Portal

* Sao chép đường dẫn repository GitHub.
* Truy cập hệ thống Portal.
* Mở bài tập Session 20 – Exercise 03.
* Dán đường dẫn repository vào phần nộp bài.
* Có thể đính kèm ảnh chụp cấu trúc repository hoặc sơ đồ IPO làm minh chứng.

8. Kết luận

Mất điện thoại chứa Google Authenticator có thể khiến lập trình viên mất quyền truy cập vào các hệ thống quan trọng như AWS. Nếu không chuẩn bị phương án khôi phục, sự cố này có thể ảnh hưởng đến quá trình bảo trì và vận hành dự án.

Việc sử dụng Backup Codes, vô hiệu hóa thiết bị MFA cũ, thiết lập thiết bị mới và cấp lại mã dự phòng là những bước quan trọng để khôi phục quyền truy cập an toàn.

Bên cạnh đó, cần lưu trữ mã khôi phục tại nơi độc lập với điện thoại, tránh lưu dưới dạng ảnh trong thư viện hoặc đồng bộ lên Cloud không được bảo vệ.

Thông điệp: Không chỉ bảo vệ thiết bị xác thực chính, lập trình viên còn phải chuẩn bị phương án dự phòng để luôn duy trì quyền kiểm soát tài khoản khi xảy ra sự cố.
