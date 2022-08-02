# Mysql

## login
```
mysql -uroot -h 127.0.0.1 -P 3306 -ppassword
```

## 导出数据库表
```sql
mysqldump -uroot -ppassword --databases db1 --tables a1 a2 >/tmp/db1.sql
```

## create database
```sql
CREATE DATABASE IF NOT EXISTS `db_linwear_data` /*!40100 DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_bin */ ;
```

## create table
```sql
CREATE TABLE `t_table` (
  `id` int(10) unsigned NOT NULL AUTO_INCREMENT,
  `created_at` datetime DEFAULT NULL,
  `updated_at` datetime DEFAULT NULL,
  `deleted_at` datetime DEFAULT NULL,
  `user_id`    varchar(128) NOT NULL COMMENT '用户ID ',
  `record_time`int(10) unsigned NOT NULL COMMENT '',  
  `medal_type` int(10) DEFAULT 1 COMMENT '',
  `status` tinyint(3) UNSIGNED DEFAULT 2 COMMENT '状态：[1:已过期][2:使用中][3:已禁用]',
  PRIMARY KEY (`id`),
  KEY `idx_user_data_medal_user_id` (`user_id`),
  KEY `idx_user_data_medal_medal_type` (`medal_type`),
  KEY `idx_user_data_medal_deleted_at` (`deleted_at`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
```

## change column
```sql
ALTER TABLE `t_table` ADD COLUMN add_column varchar(32) DEFAULT '' COMMENT '';

ALTER TABLE `t_app_send_msg_log` MODIFY COLUMN modify_column VARCHAR(1024) DEFAULT '' COMMENT '';
```


## create custom_procedure
```sql
-- 创建存储过程
DELIMITER $$

DROP PROCEDURE if EXISTS custom_procedure; 
CREATE PROCEDURE custom_procedure(IN email VARCHAR(128), IN lang VARCHAR(128))
BEGIN
	DECLARE v_id VARCHAR(128);
	DECLARE v_app_type INT;
	DECLARE account_delete_id INT;	
	SELECT id, app_type INTO v_id, v_app_type FROM t_table_1 WHERE username=email;
	if v_id = '' then
    SELECT CONCAT(email, '不存在于t_table_1');
  elseif v_id is null then
    SELECT CONCAT(email, '不存在于t_table_1');
  else
		SELECT id INTO account_delete_id FROM t_delete_table WHERE username = email AND user_id = v_id AND deletion_status = 0 ORDER BY created_at DESC LIMIT 1;
		if account_delete_id > 0 then
			SELECT CONCAT(email, '存在于t_delete_table');
		ELSE
			INSERT INTO `t_delete_table` (`created_at`, `updated_at`, `deleted_at`, `created_on`, `deleted_on`, `deletion_status`, `is_deleted_watch_data`, `user_id`, `username`, `status`, `app_type`, `account_type`, `lang`)
					VALUES (NOW(), NOW(), NULL, NOW(), '0000-00-00 00:00:00', 0, 0, v_id, email, 2, v_app_type, 1, lang);
			UPDATE `t_table_1` SET STATUS = 3 WHERE id = v_id;
			UPDATE `t_table_2` SET STATUS = 3 WHERE username = email AND user_id = v_id;
			SELECT CONCAT(email, '创建于t_delete_table');
		END if;
  END if;

END $$

DELIMITER ;

-- 调用 custom_procedure(用户名, 邮箱发送语言zh/en);
CALL custom_procedure('xx@xx.com', 'en');
```