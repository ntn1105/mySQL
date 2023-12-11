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
LEFT JOIN blog b ON c.id = b.category_id AND b.is_active = 1
LEFT JOIN news n ON c.id = n.category_id AND n.is_active = 1
WHERE b.id IS NOT NULL OR n.id IS NOT NULL;

```
### 12.	Lấy blog được tạo bởi user mà user này không có bất kỳ comment ở blog:
```
SELECT b.*
FROM blog b
JOIN user u ON b.user_id = u.id
LEFT JOIN comment c ON b.id = c.target_id AND c.target_table = 'blog' AND c.user_id = u.id
WHERE c.id IS NULL;

```
### 13.	Lấy 5 blog mới nhất và số lượng comment cho từng blog
```
SELECT b.*, COUNT(c.id) AS comment_count
FROM blog b
LEFT JOIN comment c ON b.id = c.target_id AND c.target_table = 'blog'
GROUP BY b.id
ORDER BY b.created_at DESC

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
### 23.	Lấy 2 blog, 2 news mà user có id = 1 đã comment:
```
(
b.content, b.created_at, b.updated_at
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

