# 简介

Composer是PHP中用于依赖管理的工具。它能让你定义项目中依赖的库并且将他们安装到项目中。

## 依赖管理

Composer不是一个包管理器。虽然它处理“包”和库，但是它只能管理单个项目并且安装到你的项目的一个目录下面（比如`vendor`目录）。
默认情况下它不会安装任何全局的东西。因此，它只是一个依赖管理工具。

Composer并不是一个全新的想法，它是受到了node's [npm](http://npmjs.org/)
and ruby's [bundler](http://gembundler.com/)很深的影响创造出来的。但是之前PHP中是没有这样的工具的。

Composer解决的问题如下：

a) 你有一个项目依赖于一些库。

b) 这些库中有些又依赖于另外的一些库。

c) 你定义你依赖的这些东西。

d) Composer 找出那些库的哪些版本需要被安装，并且安装他们（意思是安装到你的项目中）。


## 定义依赖

假设你创建了一个项目，你需要一个logging的库。你决定去使用[monolog](https://github.com/Seldaek/monolog).
为了在你的项目中使用它，你仅仅需要创建一个`composer.json`文件并且描述项目的依赖即可。

```json
{
    "require": {
        "monolog/monolog": "1.2.*"
    }
}
```

我们简单的说明了我们的项目依赖于一个版本始于`1.2`的`monolog/monolog`包。

## 系统需求

Composer需要到5.3.2以上的PHP上运行。一些关键的PHP设置和编译器选项是必须得，但是安装的时候将会提醒你任何不兼容的地方。

从源码安装而不是简单的zip包，你将需要git，svn和hg等工具。这取决于包得版本控制情况。

Composer是一个跨平台的工具，我们力争让它能够在Windows，Linux和OSX上都很好的工作。

## 安装到 - *nix

### 安装可执行的Composer

#### 本地安装

我们需要做两件事情来获取Composer。第一件事就是安装Composer（就是下载到你的项目中）：

```sh
curl -sS https://getcomposer.org/installer | php
```

> **注意** 如果因为某些原因是啊比了，你可以使用PHP下载安装文件：

```sh
php -r "readfile('https://getcomposer.org/installer');" | php
```

这将检查一些PHP的设置，并且下载`composer.phar`到当前工作目录。这个文件就是Composer文件。它是一个PHAR（PHP Archive）文件，
这种存档格式能够让PHP在命令行和其他一些东西执行。

你可以使用`--install-dir`选项提供一个目的地址（可以说绝对路径也可以是相对路径）把Composer安装到指定目录中：

```sh
curl -sS https://getcomposer.org/installer | php -- --install-dir=bin
```

#### 全局安装

你可以把这个文件放到任何你想要的位置。如果你把它放到`PATH`路径里面，你可以全局访问。在unixy系统你甚至可以增加可执行的权限后，不需要输入php即可执行。

你可以执行下面这个命令轻松的再系统的任何位置访问`composer`：

```sh
curl -sS https://getcomposer.org/installer | php
mv composer.phar /usr/local/bin/composer
```

> **注意：** 如果上面的命令执行失败了，请使用sudo管理员权限再次执行 `mv` 行的命令。

现在，不用 `php composer.phar`,可以仅仅执行`composer`即可。


#### 全局 (在OSX上通过 homebrew安装)

Composer是homebrew-php项目的一部分。

```sh
brew update
brew tap homebrew/homebrew-php
brew tap homebrew/dupes
brew tap homebrew/versions
brew install php55-intl
brew install homebrew/php/composer
```

## 安装到Windows上

### 使用安装文件

这是Windows上安装Composer的最简单的方式。

它将自动将最新版本的Composer安装到你的PATH环境变量中，你可以在命令行的任何目录调用`composer`。

### 手动安装

进入到一个在`PATH`环境变量的目录，并且执行安装脚本下载composer.phar：

```sh
C:\Users\username>cd C:\bin
C:\bin>php -r "readfile('https://getcomposer.org/installer');" | php
```

> **注意：** 如果因为readfile失败，请使用`http`的url 或在 php.ini开启php_openssl.dll。

在`composer.phar`文件目录下面创建一个`composer.bat`文件：

```sh
C:\bin>echo @php "%~dp0composer.phar" %*>composer.bat
```

关闭你的当前终端。在新终端里面测试：

```sh
C:\Users\username>composer -V
Composer version 27d8904
```

## 使用 Composer

我们将使用Composer给项目安装依赖。如果你没有 `composer.json` 文件在当前目录，请跳过这个 [基本使用方法](01-basic-usage.md) 章节。

运行 `install` 命令解析和下载依赖。

```sh
php composer.phar install
```

如果你全局的安装了Composer并且当前目录下面没有这个phar，你可以执行如下命令：

```sh
composer install
```

[上面的例子](#declaring-dependencies) 将下载依赖到 `vendor/monolog/monolog` 目录。

## 自动加载

除了自动下载库，Composer也准备了一个自动加载的文件，能够自动加载它下载的任何库的所有的类。在你的代码加入下面一行：

```php
require 'vendor/autoload.php';
```

哇！现在开始使用monolog！继续学习更多Composer的内容，请继续阅读 "基本使用方法" 章节。

[基本使用方法](01-basic-usage.md) &rarr;
