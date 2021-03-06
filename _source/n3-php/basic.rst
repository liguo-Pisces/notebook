PHP基础
===========

阅读官方文档
-------------------------
阅读 `PHP Document <https://www.php.net/docs.php>`_。

PHP的官方文档包含了PHP的所有的基础知识点，文档也非常详细，是学习PHP很好的教材。

* PHP的简介
* PHP的安装与配置
* PHP语法糖
* PHP扩展库文档


PHP的依赖管理工具 
-------------------------

Composer
^^^^^^^^^^^^^^^^^^^^^^^^^

**Composer** 是PHP用来管理依赖（dependency）关系的工具。你可以在自己的项目中声明所依赖的外部工具库（libraries），Composer会帮你安装这些依赖的库文件。

Composer的安装与使用在官方文档（`Composer官网 <https://getcomposer.org/>`_ | `Composer中文官网 <https://www.phpcomposer.com/>`_）中有详细的说明，需要认真的阅读。

若使用Composer下载第三方库慢，可使用中国镜像。配置方法在Composer中文官网可以找到[`传送门 <https://pkg.phpcomposer.com/>`_]。

Pear: PHP Extension and Application Repository （弃用）
^^^^^^^^^^^^^^^^^^^^^^^^^

PEAR是用于可重用PHP组件的框架和分发系统（PHP官方的）。Pear仓库代码是以包（package）区分。 **包中扩展的功能是用纯PHP代码实现的。** Pear package以phar（PHP归档）、tar或zip发布。若想了解PEAR的更多信息可以去它的 `Pear Homepage <https://pear.php.net/>`_ 。

Pear由于是全局安装扩展包，不同的项目不能使用不同的版本。因此现在基本使用Composer来作为PHP的依赖管理工具。

PECL: PHP Extension Community Library
^^^^^^^^^^^^^^^^^^^^^^^^^

扩展PHP的方法有两种：

    1. 使用纯PHP代码开发的包（package）,使用Composer或Pear管理
    2. 使用C语言编写的外部模块（extension）加载至PHP中，使用Pecl管理。

Composer或Pear是PHP的上层扩展，Pecl是PHP的底层扩展。

Pecl extension是使用C语言开发的，通常用于补充一些用PHP难以完成的底层功能，往往需要重新编译或者在配置文件中设置后才能在用户代码中使用。若想了解PECL的更多信息可以去它的 `Pecl Homepage <https://pecl.php.net/>`_ 。

PHP安装Extension的方法
^^^^^^^^^^^^^^^^^^^^^^^^^

1. 通过Pecl安装， ``pecl install extname`` （推荐）
2. 通过源码进行安装，通过 ``phpize`` 准备PHP扩展库的编译环境。具体安装步骤需要阅读PHP扩展库的安装文档。 `如何使用phpize编译共享PECL扩展库。 <https://www.php.net/manual/en/install.pecl.phpize.php>`_ （推荐）
3. 通过二进制包，一些发行版提供了预编译好的二进制包。

日志
-------------------------

在编程开发中，记录日志是一项非常重要的工作，然而记录日志很容易被程序员忽略。因此记录良好的日志是程序员必备的一项技能。

PHP有一个功能完整且容易扩展的日志类库（ `Monolog <https://github.com/Seldaek/monolog>`_ ）。Monolog能发送你的记录到文件、socket、邮箱和各式各样的Web服务中。在Monolog中的每个Logger实例都有一个channel（唯一的名字）和一个由一个或多个的Handler组成的Stack。当添加一条记录到Logger的时候，它会遍历这个Handler Stack。可以通过Handler的bubble属性来阻塞处理。有许多优秀的PHP Framework中集成了Monolog，值得学习。

最后还要牢记的一点是： **记录优良的日志非常重要**

测试 PHPUnit
-------------------------



调试 XDebug
-------------------------

开发调试的时候方法有很多，可以通过调用输出方法打印数据、记录日志和断点（Breakpoint）。不同的方法在不同的情况下都有它的优势与劣势。

调试工具（如：XDebug）能够让代码在指令组模拟器（ISS）中可以检查运行状况以及选择性地运行，以便排错、调试。当开发的进度遇到瓶颈或找不出哪里有问题时，这技术是非常有用的。但是将程序运行在调试器之下，这将比直接在运作的平台以及处理器上运行还要来的慢。因此，生产环境不会部署调试器。

大部分的主流调试工程，譬如gdb和dbx提供基于主控台的命令提示接口（console-based command line）。调试器前端应用，现在普遍是提供了集成开发工具（IDE）作为调试引擎、动态化、可视化等特点。

Xdebug是PHP的一个extension。 `安装 <https://xdebug.org/docs/install>`_ 方法在Xdebug的官方文档有说明。在这里（https://xdebug.org/wizard）可以通过phpinfo的信息查询对应Xdebug的安装信息。大部分的可配置Debug的编辑器上，都有相应配置Xdebug的说明。在配置环境的时候可以去查阅。

XDebug工作原理：

1. 客户端（IDE）中集成了遵循BGDp的Xdebug插件，当需要debug的时候，启用这个插件，这个插件会启动一个端口（默认为：9000）来监听远程服务器发过来的debug信息。
2. 浏览器向Web服务器发送一个带有 **XDEBUG_SESSION_START** 的参数请求。Web服务器需要安装的PHP的xdebug extension。
3. PHP检测到请求中含有 **XDEBUG_SESSION_START** 参数，就会告诉xdebug，xdebug会指定IP与指定Port（静态绑定Host与动态绑定Host, xdebug.remote_connect_back配置决定，默认为静态）发送一个debug请求，然后客户端响应这个请求，debug就开始了。
4. PHP就开始逐行执行代码，但是没执行一行都会让xdebug过滤一下，xdebug每过滤一行代码，都会暂停（Pause）代码的执行，然后向客户端指定端口发送该行代码的执行情况，等待客户端的决策。
5. 相应，客户端（IDE）收到xdebug发过来的信息，将会可视化的展示给开发者查阅。同时向xdebug发送下一步的操作。

**参考资料**

`XDEBUG从入门到精通 <https://segmentfault.com/a/1190000016325041>`_ 讲解了PHPStrom怎么配置XDebug
