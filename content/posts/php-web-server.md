+++
title = 'PHP 内置服务器'
date = 2024-10-23T22:17:50+08:00
draft = false
tags = [ 'PHP' ]
categories = '开发'
+++

> 官方文档: [PHP: 内置 Web Server](https://www.php.net/manual/zh/features.commandline.webserver.php)

<br>

### 什么是 PHP 内置服务器?

PHP 内置服务器是一种轻量级的 Web 服务器，可以通过命令行启动，运行 PHP 应用程序，而无需安装任何其他软件或配置任何服务器。

<br>

### 如何启动 PHP 内置服务器?
要启动 PHP 内置服务器，请打开终端并导航到包含 PHP 应用程序的目录。在这个目录下，输入以下命令：

```bash
# 在当前目录下启动 PHP 内置服务器
# 访问 http://localhost:8000 会执行当前目录下的 index.php
php -S localhost:8000

# 指定运行目录
# php -S localhost:8000 -t public

# 使用路由脚本
# php -S localhost:8000 router.php
```

这个命令将启动 PHP 内置服务器，并监听本地 8000 端口。你现在可以在浏览器中通过 http://localhost:8000 访问您的应用程序。

<br>

### Laravel 中使用 PHP 内置服务器

通过阅读源码, 可以发现 Laravel 在 `php artisan serve` 命令中, 也是使用了 PHP 内置服务器.

##### 代码节选:
```php
// vendor/laravel/framework/src/Illuminate/Foundation/Console/ServeCommand.php

/**
 * Start a new server process.
 *
 * @param  bool  $hasEnvironment
 * @return \Symfony\Component\Process\Process
 */
protected function startProcess($hasEnvironment)
{
    $process = new Process($this->serverCommand(), public_path(), collect($_ENV)->mapWithKeys(function ($value, $key) use ($hasEnvironment) {
        if ($this->option('no-reload') || ! $hasEnvironment) {
            return [$key => $value];
        }

        return in_array($key, static::$passthroughVariables) ? [$key => $value] : [$key => false];
    })->all());

    $process->start($this->handleProcessOutput());

    return $process;
}

/**
 * Get the full server command.
 *
 * @return array
 */
protected function serverCommand()
{
    $server = file_exists(base_path('server.php'))
        ? base_path('server.php')
        : __DIR__.'/../resources/server.php';

    return [
        (new PhpExecutableFinder)->find(false),
        '-S',
        $this->host().':'.$this->port(),
        $server,
    ];
}
```

`serverCommand` 方法会返回以下信息:

```php
array:4 [ 
  0 => "D:\BtSoft\php\81\php81.exe"
  1 => "-S"
  2 => "127.0.0.1:8000"
  3 => "E:\code\other\temp\vendor\laravel\framework\src\Illuminate\Foundation\Console/../resources/server.php"
]

```

再通过 `startProcess` 方法, 将上面的命令传递给 `Symfony\Component\Process\Process` 类, 并启动一个新的进程.

<br>

##### 💡 同理, 我们也可以通过在项目根目录下执行以下命令来运行 Laravel

```bash
php -S localhost:8000 -t public
```

<br>

### 总结

PHP 内置服务器为开发人员提供了一个快速、轻量级的方式来运行和测试他们的 PHP 应用程序。希望这篇文章对你有所帮助。


<br>

___👏PHP 是世界上最好的语言!___