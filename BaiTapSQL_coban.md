#### 2.	Thêm 1 dòng dữ liệu trong bất kỳ table: 
```
INSERT INTO user(id, fullname, email, `rank`, is_active, created_at)
VALUES (16, 'NhanNguyen', 'ntn110152003@gmail.com', 6, 1, NOW());

```
### 3.	Xoá và sửa1 dòng dữ liệu trong bất kỳ table nào"
```
-- Xoa
DELETE FROM user WHERE id = 16;
-- Sua
UPDATE user
SET fullname = 'NewName', email = 'newemail@example.com', `rank` = 7, is_active = 0, created_at = NOW()
WHERE id = 16;
```
### 4.	Select 10 blog mới nhất đã active:
```

SELECT *
FROM blog
WHERE is_active = 1
ORDER BY created_at DESC
LIMIT 10;

```
### 5.	Lấy 5 blog từ blog thứ 10
```
SELECT *
FROM blog
LIMIT 5
OFFSET 9;

```
### 6.	Set is_active = 0 của user có id = 3:
```
UPDATE user
SET is_active = 0
WHERE id = 3;
```
### 7.	Xoá tất cả comment của user = 2 trong blog = 5
```
DELETE FROM comment
WHERE user_id = 2 AND target_table = 'blog' AND target_id = 5;

```
### 8.	Lấy 3 blog bất kỳ (random)
```
SELECT *
FROM blog
ORDER BY RAND()
LIMIT 3;

```
### 9.	Lấy số lượng comment trung bình trên mỗi blog (Update: Lấy số lượng comment trung bình của tất cả blog):
```
SELECT AVG(count_cmt) FROM (SELECT COUNT(comment.id) count_cmt FROM blog 
	LEFT JOIN comment ON (comment.target_id = blog.id && comment.target_table = 'blog') 
    GROUP BY blog.id) avg_cmt;
```
### 10.	Lấy Category có tồn tại blog hoặc news đã active (không được lặp lại category):
```

SELECT DISTINCT c.*
FROM category c
JOIN blog b ON c.id = b.category_id AND b.is_active = 1 # list as category_blog 
JOIN news n ON c.id = n.category_id AND n.is_active = 1 # category_blog left join news => category  
WHERE b.id IS NOT NULL OR n.id IS NOT NULL;

SELECT DISTINCT * FROM category 
WHERE id IN (SELECT DISTINCT category_id FROM blog WHERE is_active = 1) 
OR id IN  (SELECT DISTINCT category_id FROM news WHERE is_active = 1);

SELECT DISTINCT * FROM category 
WHERE id IN (SELECT DISTINCT category_id FROM blog WHERE is_active = 1
union
SELECT DISTINCT category_id FROM news WHERE is_active = 1);
```
### 11.Lấy tổng lượt view của từng category thông qua blog và news
SELECT category_id, SUM(sumview) AS total_views
FROM (
    SELECT category_id, SUM(`view`) AS sumview FROM blog GROUP BY category_id
    UNION 
    SELECT category_id, SUM(`view`) AS sumview FROM news GROUP BY category_id
) AS Sum_view
GROUP BY category_id;
### 12.	Lấy blog được tạo bởi user mà user này không có bất kỳ comment ở blog:
```
SELECT * FROM blog WHERE user_id NOT IN 
	(SELECT distinct user_id FROM `comment` WHERE target_table = 'blog');

```
### 13.	Lấy 5 blog mới nhất và số lượng comment cho từng blog
```
SELECT b.*, COUNT(c.id) AS comment_count
FROM blog b
JOIN comment c ON b.id = c.target_id AND c.target_table = 'blog'
GROUP BY b.id
ORDER BY b.created_at DESC LIMIT 5;

```
### 14.Lấy 3 User comment đầu tiên trong 5 blogs mới nhất => user information
```
SELECT DISTINCT `user`.* FROM `user` WHERE id IN
	(SELECT distinct `comment`.user_id FROM `comment` 
	, (SELECT blog.* FROM blog ORDER BY created_at DESC LIMIT 5) as latest_blog 
    where `comment`.user_id = latest_blog.user_id and target_table= 'blog') LIMIT 3;
```
### 15.	Update rank user = 2 khi tổng số lượng comment của user > 20:
```
UPDATE user
SET `rank` = 2
WHERE id IN (
    SELECT user_id
    FROM comment
    GROUP BY user_id
    HAVING COUNT(user_id) > 20
);
SET SQL_SAFE_UPDATES = 0;

```
### 16.	Xoá comment mà nội dung comment có từ "fuck" hoặc "phức":
```
DELETE FROM comment
WHERE comment LIKE '%fuck%' OR comment LIKE '%phức%';

```
### 17.	Select 10 blog mới nhất được tạo bởi các user active
```
SELECT b.*
FROM blog b
JOIN user u ON b.user_id = u.id
WHERE u.is_active = 1
ORDER BY b.created_at DESC
LIMIT 10;

```
### 18.	Lấy số lượng Blog active của user có id là 1,2,4:
```
SELECT user_id, COUNT(*) AS active_blog_count
FROM blog
WHERE user_id IN (1, 2, 4) AND is_active = 1
GROUP BY user_id;

```
### 19. 
```SET @rd = (select id from category order by rand() limit 1);
(SELECT id, category_id, title FROM blog where category_id = @rd  LIMIT 5)
	UNION
(SELECT id, category_id, title FROM news where category_id = @rd LIMIT 5);

select id from category order by rand() limit 1;
```
### 20.	Lấy blog và news có lượt view nhiều nhất:
```(
    SELECT 'blog' AS type, id, title, view
    FROM blog
    ORDER BY view DESC
    LIMIT 1
)
UNION
(
    SELECT 'news' AS type, id, title, view
    FROM news
    ORDER BY view DESC
    LIMIT 1
);
```
### 21.	Lấy blog được tạo trong 3 ngày gần nhất
```
SELECT *
FROM blog
WHERE created_at >= NOW() - INTERVAL 3 DAY
ORDER BY created_at DESC;

```
###  22.Lấy danh sách user đã comment trong 2 blog mới nhất
```
SELECT DISTINCT u.*
FROM user u
JOIN comment c ON u.id = c.user_id
JOIN (
    SELECT id
    FROM blog
    ORDER BY created_at DESC
    LIMIT 2
) b ON c.target_table = 'blog' AND c.target_id = b.id;

```
### 23.	Lấy 2 blog, 2 news mà user có id = 1 đã comment:
```
(
	SELECT 'blog' AS type, b.id, b.category_id, b.user_id, b.title, b.view, b.is_active, b.content, b.created_at, b.updated_at
    FROM blog b
    JOIN comment c ON b.id = c.target_id AND c.target_table = 'blog'
    WHERE c.user_id = 1
    LIMIT 2
)
UNION
(
  SELECT 'news' AS type, n.id, n.category_id, n.user_id, n.title, n.view, n.is_active, n.content, n.created_at, n.updated_at
    FROM news n
    JOIN comment c ON n.id = c.target_id AND c.target_table = 'news'
    WHERE c.user_id = 1
    LIMIT 2
);


```
### 24.	Lấy 1 blog và 1 news có số lượng comment nhiều nhất:
```
(
    SELECT 'blog' AS type, b.id, b.title, b.view, b.is_active, b.content, b.created_at, b.updated_at, COUNT(c.id) AS comment_count
    FROM blog b
    JOIN comment c ON b.id = c.target_id AND c.target_table = 'blog'
    GROUP BY b.id
    ORDER BY comment_count DESC
    LIMIT 1
)
UNION
(
    SELECT 'news' AS type, n.id, n.title, n.view, n.is_active, n.content, n.created_at, n.updated_at, COUNT(c.id) AS comment_count
    FROM news n
	JOIN comment c ON n.id = c.target_id AND c.target_table = 'news'
    GROUP BY n.id
    ORDER BY comment_count DESC
    LIMIT 1
);

```
### 25.	Lấy 5 blog và 5 news mới nhất đã active
```
(
    SELECT 'blog' AS type, b.id, b.category_id, b.user_id, b.title, b.view, b.is_active, b.content, b.created_at, b.updated_at
    FROM blog b
    WHERE b.is_active = 1
    ORDER BY b.created_at DESC
    LIMIT 5
)
UNION
(
    SELECT 'news' AS type, n.id, n.category_id, n.user_id, n.title, n.view, n.is_active, n.content, n.created_at, n.updated_at
    FROM news n
    WHERE n.is_active = 1
    ORDER BY n.created_at DESC
    LIMIT 5
);

```
### 26.	Lấy nội dung comment trong blog và news của user id =1
```
(
    SELECT 'blog' AS type, b.title, c.comment
    FROM blog b
    JOIN comment c ON b.id = c.target_id AND c.target_table = 'blog'
    WHERE c.user_id = 1
)
UNION
(
    SELECT 'news' AS type, n.title, c.comment
    FROM news n
    JOIN comment c ON n.id = c.target_id AND c.target_table = 'news'
    WHERE c.user_id = 1
);

```
### 27.	Blog của user đang được user có id = 1 follow:
```
SELECT b.*
FROM blog b
JOIN follow f ON b.user_id = f.to_user_id
WHERE f.from_user_id = 1;

```
### 28.	Lấy số lượng user đang follow user = 1:
```
SELECT COUNT(*) AS follow_count
FROM follow
WHERE to_user_id = 1;

```
### 29. Lấy số lượng user 1 đang follow
```
SELECT COUNT(*) AS followers_count
FROM follow
WHERE to_user_id = 1;

```
### 30.	Lấy 1 comment(id_comment, comment) mới nhất và thông tin user của user đang được follow bởi user 1
```
SELECT c.id AS id_comment, c.comment, u.*
FROM comment c
JOIN user u ON c.user_id = u.id
WHERE c.user_id IN (
    SELECT from_user_id
    FROM follow
    WHERE to_user_id = 1
)
ORDER BY c.created_at DESC
LIMIT 1;

```
### 31.	Hiển thị một chuổi "PHP Team " + ngày giờ hiện tại (Ex: PHP Team 2017-06-21 13:06:37)
```
SELECT CONCAT('PHP Team ', NOW()) AS result;
```
### 32.	Tìm có tên(user.full_name) "Khiêu" và các thông tin trên blog của user này như: (blog.title, blog.view), title category(category) của blog này. Hiển thị theo output như bên dưới:
![Hình minh họa](https://scontent.fdad3-5.fna.fbcdn.net/v/t1.15752-9/400410512_7132196923531529_5906186640129939862_n.png?_nc_cat=106&ccb=1-7&_nc_sid=8cd0a2&_nc_ohc=-Z1is8fR64cAX8F1y3V&_nc_ht=scontent.fdad3-5.fna&oh=03_AdRYtEviXgcWSNe5w6ng4mYK4UBOsPZg8dqMK41BtMUZJQ&oe=659E0306
)
```
SELECT u.fullname AS fullname, b.title AS itle, b.view AS view, c.title AS category
FROM user u
JOIN blog b ON u.id = b.user_id
JOIN category c ON b.category_id = c.id
WHERE u.fullname LIKE '%Khiêu%';

```
### 33. Liệt kê email user các user có tên(user.full_name) có chứa ký tự "Khi" theo danh sách như output bên dưới.

![a](https://scontent-lax3-2.xx.fbcdn.net/v/t1.15752-9/406942879_925314832561954_6034811567382879009_n.png?_nc_cat=106&ccb=1-7&_nc_sid=510075&_nc_ohc=7PYN2pttDKIAX8_ARMN&_nc_ad=z-m&_nc_cid=0&_nc_ht=scontent-lax3-2.xx&oh=03_AdQgOfMINQm4epcPWMLpeRoVVu0eiGS7Y-OBuv8GWel3gw&oe=659DF667)
```
SELECT GROUP_CONCAT(email) AS emails
FROM user
WHERE fullname LIKE '%Khi%';


```
### Câu chưa làm :34
