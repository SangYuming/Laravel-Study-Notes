# Study Laravel Notes

> author : SangYuming

### 一、Xampp配置

- 配置虚拟站点

  1. 确保xampp/httpd.conf下"*Include conf/extra/httpd-vhosts.conf*"前面没有**#**号

  2. 在虚拟主机设置文件xampp\apache\conf\extra\httpd-vhosts.conf里设置：

     ```conf
     <VirtualHost *:80>
         DocumentRoot "E:/xampp/htdocs/laravelapp/public"
         ServerName laravel.app
         ErrorLog "logs/laravelapp-error.log"
         CustomLog "logs/laravelapp-access.log" common
     </VirtualHost>
     ```

     注：解决了url中需要输入public进入



## 二、Laravel安装



## 三、数据库配置

- 配置.env文件

  ```
  DB_CONNECTION=mysql
  DB_HOST=127.0.0.1
  DB_PORT=3306
  DB_DATABASE=laraveltest
  DB_USERNAME=root
  DB_PASSWORD=
  ```

- 验证配置成功

  - 输入命令安装表migrations,这个表主要用来追踪哪些迁移已经运行了

    ```
    php artisan migrate:install
    ```

  注：要确保目录在Laravel内

## 四、命名空间

- php中的命名空间
  - 命名空间解决以下两个问题：
    1. 防止代码与PHP内部的类/函数/常量或第三方类/函数/常量之间的**名字冲突**
    2. 为解决第一种问题标识符很长，命名空间可创建简短易懂的名称，**提高代码可读性**
  - 定义命名空间
    1. 命名空间只影响类（包括抽象类和traits）、接口、函数和常量
    2. ​
- Laravel中的命名空间

## 五、路由

- 路由响应HTTP请求

  ```php
  <?php
    Route::get($uri, $callback);
    Route::post($uri, $callback);
    Route::put($uri, $callback);
    Route::patch($uri, $callback);
    Route::delete($uri, $callback);
    Route::options($uri, $callback); 
  ?>
  ```

  ​


- 路由的几种方式

  第一种方式:**闭包**

  ```php
  <?php
    Route::get('/', function () {
      return view('welcome');
  });
  ```

  第二种方式:



## 六、Controller

### 1、Controller的创建

- 创建的目录：App\Http\Controllers;


- 使用命令行创建Controller

  ```
  php artisan make:controller PostController
  ```





### 2、Controller调用模板及传参

- 调用模板

  ```php
  <?php
    //view函数用以调用模板，会找到resources/views中的模板
    //因为找到模板的路径为post/index,会找到views中public文件夹中的index.blade.php模板,书写时写上blade前的名称即可
    return view('post/index');
  ```

- 向模板传参

  第一种方法：（及关联数组传参）

  ```php
  <?php
  view('post/index',[数组]);
  ```

  ```php
  <?php
  $posts = [
              ['title' => 'this is title1'],
              ['title' => 'this is title2'],
              ['title' => 'this is title3']
          ];
  return view('post/index',['posts'=>$posts]);//要传递的变量名和写的变量名要尽量保持一致，便于找错误
  ```

  第二种方法：(compact方法传参)

  **compact()函数**：创建一个包含变量名和它们的值的数组。

  compact英文意思：n:协议条约  adj:紧凑的  vt&vi:压紧

  ```php
  <?php
  $posts = [
              ['title' => 'this is title1'],
              ['title' => 'this is title2'],
              ['title' => 'this is title3']
          ];
  return view('post/index',compact('posts'));
  ```

  ​

  ​



## 七、模板blade

### 1、模板语法



###  问题收集

- 注意看 Controller中 view的路径，他找到的更目录是resources/views

- 模板中的css和js、images等都放在public文件中

- 在模板使用时导入css、js等，应该这样写

  ```html
  <link href="/css/blog.css" rel="stylesheet">
  <!--js雷同-->
  ```

  ​



## 数据库迁移

### 1、创建migration

```
php artisan make:migration create_posts_table
```

