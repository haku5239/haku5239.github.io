---
 title: 防止sql注入 
 date: 2020-03-26 17:47:15 
 tags: 
 - blog 
 - mysql
 categories: 
---

### 防止sql注入 

```php
$id = $_POST['id'];
mysql_query('select * from users where id = '. $id);
// 当用户恶意注入时，就很危险
// 例如： $id的值为：1;Drop table users;--
// 拼接sql后为：select * from users where id = 1;Drop table users;--
```

为防止sql注入，可以使用`PDO`的预处理

```php
$sql = $pdo->prepare('select * from users where id = ?');
$sql->execute([$_POST['id']]);
```

