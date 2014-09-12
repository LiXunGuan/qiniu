# 七牛云 sdk for laravel

[七牛云存储](http://qiniu.com)非官方SDK，采用[PSR规范](https://github.com/hfcorriez/fig-standards)，支持[Composer](http://getcomposer.org)安装


# 安装

添加 `"lixunguan/qiniu": "*"` 到 [`composer.json`](http://getcomposer.org).

```
composer.phar install

打开app.php 给aliases  加上  'Qiniu'  => 'Lixunguan\Qiniu\Storage'
```

# 引导



- [资源管理](#资源管理)
  - [查看文件](#查看文件)
  - [复制文件](#复制文件)
  - [移动文件(重命名)](#移动文件)
  - [删除文件](#删除文件)
  - [筛选文件](#筛选文件)
  - [上传文件](#上传文件)
  - [下载文件](#下载文件)


## 资源管理
### 查看文件

```php
	return Qiniu::make(array(
		'access_key' => Config::get('app.upload_access_key'),
		'secret_key' => Config::get('app.upload_secret_key'),
		'bucket'     => Config::get('app.upload_bucket')
	))->info('uploads/2014/0910/31c0497aefbf45a22822e9761660a61e.jpg');
```

输出

```
Array
(
    [fsize] => 69478
    [hash] => FkkMiEQKOsHOAkQOsA0zZ8Noxsf2
    [mimeType] => image/jpeg
    [putTime] => 1.4103365664006E+16
)
```

### 复制文件

```php
	return Qiniu::make(array(
		'access_key' => Config::get('app.upload_access_key'),
		'secret_key' => Config::get('app.upload_secret_key'),
		'bucket'     => Config::get('app.upload_bucket')
	))->copy('uploads/2014/0910/31c0497aefbf45a22822e9761660a61e.jpg', 'new.jpg');
```

输出

```
	如果请求成功，不返回任何内容。
	如果请求失败，返回包含如下内容:
	Array(
		[code]  => HTTP状态码
		[error] => 与HTTP状态码对应的消息文本
	)
```

### 移动文件

```php
	return Qiniu::make(array(
		'access_key' => Config::get('app.upload_access_key'),
		'secret_key' => Config::get('app.upload_secret_key'),
		'bucket'     => Config::get('app.upload_bucket')
	))->move('new.jpg', 'move.jpg');
```

输出

```
	如果请求成功，不返回任何内容。
	如果请求失败，返回包含如下内容:
	Array(
		[code]  => HTTP状态码
		[error] => 与HTTP状态码对应的消息文本
	)
```

### 删除文件

```php
	return Qiniu::make(array(
		'access_key' => Config::get('app.upload_access_key'),
		'secret_key' => Config::get('app.upload_secret_key'),
		'bucket'     => Config::get('app.upload_bucket')
	))->delete('new.jpg');
```

输出

```
	如果请求成功，不返回任何内容。
	如果请求失败，返回包含如下内容:
	Array(
		[code]  => HTTP状态码
		[error] => 与HTTP状态码对应的消息文本
	)
```

### 筛选文件

```php
	return Qiniu::make(array(
		'access_key' => Config::get('app.upload_access_key'),
		'secret_key' => Config::get('app.upload_secret_key'),
		'bucket'     => Config::get('app.upload_bucket')
	))->lists(array('prefix' => 'uploads/2010')); // 指定前缀搜索
```

### 上传文件

```php
	return Qiniu::make(array(
		'access_key' => Config::get('app.upload_access_key'),
		'secret_key' => Config::get('app.upload_secret_key'),
		'bucket'     => Config::get('app.upload_bucket')
	))->upload('123.jpg', 'uploads/123.jpg');
```

### 下载文件

```php
	return Qiniu::make(array(
		'access_key' => Config::get('app.upload_access_key'),
		'secret_key' => Config::get('app.upload_secret_key'),
		'bucket'     => Config::get('app.upload_bucket')
	))->download($value, true); // true 为私有文件
```
