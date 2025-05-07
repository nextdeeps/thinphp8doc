# cacheAlways

`cacheAlways`的使用方法与`cache`一样,只不过在最终表现中,如果本次查询数据为空,那么`cache`不会缓存,而`cacheAlways`会把这次`空数据`缓存下来,下次查询的时候会直接返回`空数据`.
```php

    Db::table('user')->cacheAlways('key',60,'tagName')->where('username','think')->find();
    

```
