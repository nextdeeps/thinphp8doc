# Trace调试

调试模式并不能完全满足我们调试的需要，有时候我们需要手动的输出一些调试信息。除了本身可以借助一些开发工具进行调试外，ThinkPHP还提供了一些内置的调试工具和函数。
`Trace`调试功能就是ThinkPHP提供给开发人员的一个用于开发调试的辅助工具。可以实时显示当前页面或者请求的请求信息、运行情况、SQL执行、错误信息和调试信息等，并支持自定义显示，并且支持没有页面输出的操作调试。最新版本页面Trace功能已经不再内置在核心，但默认安装的时候会自动安装`topthink/think-trace`扩展，所以你可以在项目里面直接使用。
如果部署到服务器的话，你可以通过下面方式安装
```php

    composer install --no-dev
    

```
就不会安装页面Trace扩展。
## 使用
> 页面Trace功能仅在调试模式下有效
安装页面Trace扩展后，如果开启调试模式并且运行后有页面有输出的话，页面右下角会显示`ThinkPHP`的LOGO：
![](https://doc.thinkphp.cn/lfs/07f8ea0efed5d4c85c4a168909fd26cdf5746a792cd3f480d97cc15fd2e0ad4a.dat)
LOGO后面的数字就是当前页面的执行时间（单位是秒） 点击该图标后，会展开详细的Trace信息，如图：
![](https://doc.thinkphp.cn/lfs/beb4728c45443d36582ed2881a868f26dc5975e59da3f59df9989b59f2ecdca5.dat)
Trace框架有6个选项卡，分别是基本、文件、流程、错误、SQL和调试，点击不同的选项卡会切换到不同的Trace信息窗口。
选项卡| 描述  
---|---  
基本| 当前页面的基本摘要信息，例如执行时间、内存开销、文件加载数、查询次数等等  
文件| 详细列出当前页面执行过程中加载的文件及其大小  
流程| 会列出当前页面执行到的行为和相关流程  
错误| 当前页面执行过程中的一些错误信息，包括警告错误  
SQL| 当前页面执行到的SQL语句信息  
调试| 开发人员在程序中进行的调试输出  
Trace的选项卡是可以定制和扩展的，如果你希望增加新的选项卡，则可以修改配置目录下的`trace.php`文件中的配置参数如下：
```php

    return [
        'type' => 'Html',
        'tabs' => [
            'base'  => '基本',
            'file'  => '文件',
            'info'  => '流程',
            'error' => '错误',
            'sql'   => 'SQL',
            'debug' => '调试',
            'user'  => '用户',
        ],
    ];
    

```
> `base`和`file`是系统内置的，其它的选项其实都属于日志的等级（user是用户自定义的日志等级）。
也可以把某几个选项卡合并，例如：
```php

    return [
        'type' => 'Html',
        'tabs' => [
            'base'                 => '基本',
            'file'                 => '文件',
            'error|notice|warning' => '错误',
            'sql'                  => 'SQL',
            'debug|info'           => '调试',
        ],
    ];
    

```
更改后的Trace显示效果如图：
![](https://doc.thinkphp.cn/lfs/ad56a1ba3ce9f4d56f2c714566bc7fbf9b0f9104c7e804f1da719f0002636d78.dat)
如果需要更改页面Trace输出的样式，可以自定义模板文件（可以复制内置模板文件`vendor/topthink/think-trace/src/tpl/page_trace.tpl`的内容），然后配置`file`参数指定模板文件位置。
```php

    'file'    =>    'app\trace\page_trace.html',
    

```
## 浏览器控制台输出
trace功能支持在浏览器的`console`直接输出，这样可以方便没有页面输出的操作功能调试，只需要在配置文件中设置：
```php

        // 使用浏览器console输出trace信息
        'type'  =>  'console',
    

```
运行后打开浏览器的console控制台可以看到如图所示的信息：
![](https://doc.thinkphp.cn/lfs/f7683d4707211883b160296e0f70ca39582248ed0934fb01bf514b9b6cf04a0d.dat)
浏览器Trace输出同样支持`tabs`设置。
> 由于页面Trace功能是通过中间件来执行，所以命令行下面不会显示任何的页面Trace信息
