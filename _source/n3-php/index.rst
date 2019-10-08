什么是PHP？
==========

PHP (recursive acronym for PHP: Hypertext Preprocessor) is a widely-used open source general-purpose scripting language that is especially suited for web development and can be embedded into HTML.

PHP（“PHP: Hypertext Preprocessor”，超文本预处理器的字母缩写）是一种被广泛应用的开放源代码的多用途脚本语言，它可嵌入到 HTML中，尤其适合 web 开发。

解释型语言（Interpreted language）
-----------------------------

解释型语言（Interpreted language）是一种编程语言类型。这种类型的编程语言，会将代码一句一句直接运行，不需要像编译语言（Compiled language）一样，经过编译器先行编译为机器代码，之后再运行。这种编程语言需要利用解释器，在运行期，动态将代码逐句解释（interpret）为机器代码，或是已经预先编译为机器代码的的子程序，之后再运行。

理论上，任何编程语言都可以是编译式，或解释型的。它们之间的区别，仅与程序的应用有关。许多编程语言同时采用编译器与解释器来实现，其中包括Lisp，Pascal，C，BASIC 与 Python。JAVA及C#采用混合方式，先将代码编译为字节码，在运行时再进行解释。

PHP执行过程需先编译成中间代码（opcode），再经由特定的虚拟机，翻译成特定的指令被执行。其执行过程如下：

.. code-block:: console

    PHP5: PHP code -> Token -> Opcodes -> Execute
    PHP7: PHP code -> Token -> AST -> Opcodes -> Execute

    1. Token是PHP代码被分割成的有意义的标识。
    2. AST（Abstract Syntax Tree, 抽象语法树）是PHP7版本的特性，之前版本的PHP代码执行过程中没有这一步。它的作用主要是实现了PHP编译器和解析器的解耦，提升了可维护性。
    3. 将AST转化为Opcode，Opcode才能被引擎执行。
    4. Opcodes是Opcode的集合形式，是PHP执行过程中的中间代码。PHP可以通过opcache来缓存Opcodes。通过省去源码到opcode的阶段，引擎直接执行缓存好的Opcode，以提升性能。

动态编程语言（Dynamic programming language）
-----------------------------

计算机科学中的动态编程语言是一类高级编程语言，它们在运行时执行静态编程语言在编译过程中执行的许多常见编程行为。这些行为可能包括程序的扩展，添加新的代码，扩展对象和定义或修改数据类型。

动态语言实现的一些特性：

* Eval： 一些动态语言提供了Eval的功能。此函数可以执行一个包含该语言代码的字符串。不建议使用该特性。
* Object runtime alteration： 类型或者对象通常可以在运行时动态的进行修改。
* Reflection： 反射是指计算机程序在运行时可以访问、检测和修改它本身状态或行为的一种能力。
* Macros： 宏在C或C++中是一种静态功能，只能在程序文本上进行字符串替换。但是，在动态语言中，它们提供对编译器内部的访问，并提供对解析器，虚拟机或运行时的完全访问，从而允许定义类型语言的结构，这些结构可以优化代码或修改程序的语法。（TODO）

弱类型（weakly typed）
-----------------------------

强弱类型（Strong and weak typing）表示在计算机科学以及程序设计中，经常把编程语言的类型系统分为强类型（英语：strongly typed）和弱类型（英语：weakly typed (loosely typed)）两种。这两个术语并没有非常明确的定义，但主要用以描述编程语言对于混入不同数据类型的值进行运算时的处理方式。强类型的语言遇到函数引数类型和实际调用类型不符合的情况经常会直接出错或者编译失败；而弱类型的语言常常会实行隐式转换，或者产生难以意料的结果。

PHP是弱类型语言，优点是开发效率比较高。

弱类型语言的缺点比较多。主要体现在：

    * 不符合 “`所见即所得（WYSIWYG） <https://zh.wikipedia.org/wiki/%E6%89%80%E8%A6%8B%E5%8D%B3%E6%89%80%E5%BE%97>`_” 的设计思路，定义的变量类型是不可预见性并且可以改变的。
    * 变量的类型是不可控的，因此执行过程中拥有大量的变量类型 “隐式转换” ，在开发同学不清楚隐式转换规则的情况下，容易产生不可预知的结果。

PHP7提供了类型声明的特性，可以指定函数参数的类型与返回值的类型。

PHP内核
-----------------------------

* 解释器（interpreter）

解释器是一种程序，能够把编程语言一行一行解释运行。解释器像是一位“中间人”，每次运行程序时都要先转换成另一种语言再作运行，因此解释器的程序运行速度比较缓慢。它不会一次把整个程序翻译出来，而是每翻译一行程序叙述就立刻运行，然后再翻译下一行，再运行，如此不停地进行下去。

* PHP运行机制



.. [:ref:`AST` ] https://zh.wikipedia.org/wiki/%E6%8A%BD%E8%B1%A1%E8%AA%9E%E6%B3%95%E6%A8%B9
https://en.wikipedia.org/wiki/Dynamic_programming_language
http://www.php-internals.com/book/?p=index
