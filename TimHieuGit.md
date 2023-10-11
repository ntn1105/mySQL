## Git là gì ? 
Git là một hệ thống quản lý phiên bản phân tán (DVCS - Distributed Version Control System) được sử dụng để theo dõi và quản lý sự thay đổi trong mã nguồn của một dự án phần mềm. Git cho phép nhiều người làm việc trên cùng một dự án, theo dõi lịch sử thay đổi, và hợp nhất (merge) các thay đổi từ nhiều nguồn khác nhau.
## Đặc điểm của git:
- **Hệ thống phân tán:** Mọi người dùng có bản sao đầy đủ của toàn bộ dự án trên máy của họ.
- **Lịch sử thay đổi:** Git lưu trữ mọi thay đổi trong dự án, giúp dễ dàng xem lịch sử và quay lại phiên bản cũ.
- **Nhánh (branch):** Git cho phép tạo và quản lý các nhánh riêng để phát triển tính năng, sửa lỗi mà không ảnh hưởng đến phiên bản chính.
- **Hợp nhất (merge):** Có thể hợp nhất các thay đổi từ nhiều nhánh khác nhau vào nhánh chính.
- **Hiệu suất nhanh:** Git hoạt động nhanh chóng, kể cả với các dự án lớn.
## Tại sao phải sử dụng git:
*Git có nhiều lợi ích, bao gồm:*
- **Quản lý lịch sử:** Theo dõi lịch sử thay đổi dự án.
- **Hợp nhất dễ dàng:** Hợp nhất thay đổi từ nhiều nguồn một cách hiệu quả.
- **Làm việc đồng thời:** Cho phép nhiều người làm việc trên cùng một dự án.
- **Quản lý nhánh:** Tạo và quản lý các nhánh để phát triển tính năng và sửa lỗi mà không ảnh hưởng đến phiên bản chính.
- **Sao lưu dự án:** Làm sao lưu dự án để tránh mất dữ liệu quan trọng.
## 	Cách cài đặt git?
Bạn có thể cài đặt Git bằng cách tải trực tiếp từ trang web chính thức của Git
***[Download Git](https://git-scm.com/downloads)***
## Github là gì ?
GitHub là một dịch vụ lưu trữ mã nguồn trực tuyến dựa trên Git. Nó cung cấp một nền tảng để lưu trữ, quản lý và hợp nhất mã nguồn, cho phép nhiều người làm việc cùng một dự án. GitHub cũng cung cấp nhiều tính năng xã hội và quản lý dự án, bao gồm theo dõi vấn đề, tạo wiki, và tích hợp liên kết với các dịch vụ khác.

## Repository là gì? Các tạo ra 1 Repository.
Repository (hay repo) là nơi lưu trữ tất cả các tệp và lịch sử thay đổi của một dự án trong Git. Để tạo một repository trên Git, bạn có thể làm theo các bước sau:

- Đăng nhập vào tài khoản GitHub của bạn.
- Trên trang chính, nhấn vào nút "New" hoặc "Create repository."
- Đặt tên cho repository, chọn quyền riêng tư (public hoặc private), và thêm mô tả (nếu cần).
- Chọn các tùy chọn bổ sung, như tạo README.md hoặc gitignore.
- Nhấn nút "Create repository" để tạo.
## Phân biệt local branch và remote branch?
- **Local branch:** Là nhánh trên máy tính cá nhân của bạn, được sử dụng để phát triển và thử nghiệm tính năng.
- **Remote branch:** Là nhánh trên máy chủ từ xa (như GitHub), chứa phiên bản chính của dự án. Remote branch được chia sẻ giữa nhiều người làm việc trên dự án và là nơi hợp nhất (merge) các thay đổi từ nhiều nguồn khác nhau.
## Git clone, push, pull, fetch, merge, add, commit?
- **Git clone:** Sao chép một repository từ máy chủ từ xa vào máy tính cá nhân của bạn.
- **Git push:** Đẩy các thay đổi từ local repository lên remote repository để chia sẻ với người khác.
- **Git pull:** Kết hợp git fetch và git merge để lấy các thay đổi từ remote repository và cập nhật local repository.
- **Git fetch:** Lấy thông tin từ remote repository như các thay đổi mới mà không thực hiện hợp nhất.
- **Git merge:** Hợp nhất các thay đổi từ một branch khác vào branch hiện tại.
- **Git add:** Đánh dấu các thay đổi cho việc commit trong local repository.
- **Git commit:** Lưu trạng thái hiện tại của local repository vào lịch sử với một thông điệp mô tả.
## Các trạng thái của files trong git là gì? 
*Có ba trạng thái chính của các tệp trong Git:*

- **Untracked (Chưa được theo dõi):** Các tệp mới được thêm vào thư mục là untracked. Git không theo dõi chúng.
- **Tracked (Được theo dõi):** Các tệp đã được thêm vào local repository và được theo dõi bởi Git.
- **Staged (Được đánh dấu):** Các tệp đã được đánh dấu để thêm vào commit nhưng chưa được commit.
## Conflict trong git là gì? Tại sao lại xảy ra conflict? Cách giải quyết như thế nào?
Conflict trong Git xảy ra khi hai hoặc nhiều người cùng sửa đổi cùng một phần của tệp hoặc nhánh và cố gắng hợp nhất chúng. Điều này xảy ra khi Git không thể tự động hợp nhất các thay đổi vì chúng xung đột với nhau.

Để giải quyết conflict, bạn cần thực hiện các bước sau:
1. Mở tệp có conflict bằng trình soạn thảo và sửa chữa các phần bị conflict.
2. Lưu tệp sau khi sửa đổi và thêm nó vào staged area bằng lệnh git add.
3. Tiếp theo, thực hiện commit để hoàn thành quá trình hợp nhất.
4. Sau đó, push thay đổi lên remote repository.

Sau khi các conflict được giải quyết, dự án sẽ tiếp tục phát triển bình thường.