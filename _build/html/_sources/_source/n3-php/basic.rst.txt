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