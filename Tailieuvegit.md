# Nội dung bài học :
 ## 1. Giới thiệu khái quát về git : 
 -  là một hệ thống quản lý được sử dụng để theo dõi và quản lý sự thay đổi trong mã nguồn của một dự án phần mềm.
 ## 2. Các trạng thái:
 - Trong git có hai loại trạng thái chính đó là Tracked và Untracked, cụ thể: Tracked – Là tập tin đã được đánh dấu theo dõi trong Git để bạn làm việc với nó. Và trạng thái Tracked nó sẽ có thêm các trạng thái phụ khác là Unmodified (chưa chỉnh sửa gì), Modified (đã chỉnh sửa) và Staged (đã sẵn sàng để commit)
 ## 3. Các cú pháp cơ bản của git :
 - git config : dùng để cấu hình cho một file .
 - git init : tạo ra một khởi tạo một để chứa các mã nguồn mà mình thao tác với gỉt.
 - git add : chuyển file từ trạng thái đang làm việc sang trạng thái stagging.
 - git commit -m "description" : chuyển file từ trạng thái stagiing sang commited.
 - git push <remote> <branch> : dùng để đẩy các file ở dưới local lên remote (origin).
 - git pull <remote> <branch> : dùng để kéo các file từ remote (origin) về local .
 - echo "#content" >> "filename" : tạo ra file có tên là "filename" và ghi nội dung "#content" vào trong đó.
 - git fetch : Lệnh git fetch tìm nạp các bản sao và tải xuống tất cả các tệp branch về local.
- git log : kiểm tra các phiên bản đã commit .
- git status : kiểm tra trạng thái của các file .
- git reset --hard:di chuyển HEAD đến một commit cụ thể và xóa tất cả các thay đổi chưa được commit trong working directory và staging area mà không thể phục hồi.
- git reset --mixed: di chuyển HEAD đến một commit cụ thể và giữ lại các thay đổi trong working directory mà không thêm vào staging area.
- git reset --soft : di chuyển HEAD đến một commit cụ thể và giữ lại các thay đổi trong working directory và thêm vào staging area.   
- git branch : kiểm tra có bao nhiêu nhánh và mình đang ở nhánh nào.
- git checkout:trong Git được sử dụng để chuyển đổi giữa các nhánh, di chuyển đến một commit cụ thể hoặc khôi phục tệp từ commit trước đó.
- git stash save : được sử dụng để lưu trữ tạm thời các thay đổi chưa commit để bạn có thể làm việc trên một nhánh khác mà không cần commit những thay đổi đó (ngoại trừ các file untracked).
- git stash apply: lấy file ra và dán vào nhưng không làm mất file trong list.
- git stash pop : lấy file ra và dán vào và xóa file trong list.
- git cherry pick : là lệnh để áp dụng một commit cụ thể từ một nhánh khác vào nhánh hiện tại.
## 4. Các tạo ra một new reposity :
- Để tạo một repository mới trên GitHub, bạn cần đăng nhập vào tài khoản của mình, sau đó nhấp vào nút "New" ở góc phải trên cùng của trang web. Sau đó, bạn cần điền thông tin cần thiết và nhấp vào nút "Create repository" để tạo repository mới.