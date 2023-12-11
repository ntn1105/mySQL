CREATE TABLE user (
    id INT PRIMARY KEY,
    fullname VARCHAR(255),
    email VARCHAR(255),
    rank TINYINT,
    is_active TINYINT(1),
    created_at TIMESTAMP
);
CREATE TABLE category (
    id INT PRIMARY KEY,
    title VARCHAR(255),
    created_at TIMESTAMP
);
CREATE TABLE comment (
    id INT PRIMARY KEY,
    target_table VARCHAR(20),
    target_id INT,
    user_id INT,
    comment TEXT,
    created_at TIMESTAMP,
    updated_at TIMESTAMP
);
CREATE TABLE follow (
    id INT PRIMARY KEY,
    from_user_id INT,
    to_user_id INT,
    created_at TIMESTAMP
);
CREATE TABLE blog (
    id INT PRIMARY KEY,
    category_id INT,
    user_id INT,
    title VARCHAR(255),
    view INT,
    is_active TINYINT(1),
    content TEXT,
    created_at TIMESTAMP,
    updated_at TIMESTAMP
);
CREATE TABLE news (
    id INT PRIMARY KEY,
    category_id INT,
    title VARCHAR(255),
    view INT,
    is_active TINYINT(1),
    content TEXT,
    created_at TIMESTAMP,
    updated_at TIMESTAMP
);
