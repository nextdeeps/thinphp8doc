# distinct

DISTINCT 方法用于返回唯一不同的值 。
例如数据库表中有以下数据
![](https://doc.thinkphp.cn/lfs/e2c5f7b82b93d925d9f4c19383a611c90e826dc982f5478fade6afa64999b2f9.dat)
以下代码会返回`user_login`字段不同的数据
```php

    Db::table('think_user')->distinct(true)->field('user_login')->select();
    

```
生成的SQL语句是：
```php

    SELECT DISTINCT user_login FROM think_user
    

```
返回以下数组
```php

    array(2) {
      [0] => array(1) {
        ["user_login"] => string(7) "chunice"
      }
      [1] => array(1) {
        ["user_login"] => string(5) "admin"
      }
    }
    

```
`distinct`方法的参数是一个布尔值。
