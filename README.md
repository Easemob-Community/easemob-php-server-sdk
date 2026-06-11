# Easemob PHP SDK

环信 IM [服务端 API](https://docs-im.easemob.com/im/server/ready/intro) PHP 封装，节省服务器端开发者对接环信 API 的时间，只需配置 appkey 相关信息即可使用。

## 功能

PHP SDK 提供了用户、消息、群组、聊天室等资源的操作管理能力。

## 环境要求

- PHP >= 5.3.3

## 安装

```bash
composer require easemob-community/easemob-php
```

## 目录结构

| 目录 | 说明 |
|---|---|
| `src/` | 核心源码 |
| `tests/` | 测试文件 |
| `examples/` | 使用示例 |
| `runtime/` | 临时文件、Token 缓存目录 |

## 准备

在使用之前，需要准备环信 `appKey`、`Client ID`、`ClientSecret`。

- 已有账号：登录 [环信管理后台](https://console.easemob.com/user/login) → 应用列表 → 查看
- 没有账号：[注册](https://console.easemob.com/user/register) → 添加应用 → 查看

## 快速开始

使用所有类之前，先初始化 `Auth` 对象，再将其传入其他类：

```php
require 'vendor/autoload.php';

use Easemob\Auth;
use Easemob\User;

$auth = new Auth("appKey", "Client ID", "ClientSecret");
$user = new User($auth);
```

> 框架用户（Laravel / Yii / ThinkPHP）无需手动引入 `autoload.php`。

## API 模块

| 类 | 用途 |
|---|---|
| `User` | 管理用户（注册、删除、改密等） |
| `Contact` | 管理联系人（添加好友等） |
| `Group` | 管理群组 |
| `Room` | 管理聊天室 |
| `Message` | 发送消息 |
| `Attachment` | 上传下载附件 |
| `Block` | 黑名单 / 禁言 / 封禁 |
| `WhiteList` | 白名单管理 |
| `Push` | 推送设置（免打扰等） |
| `UserMetadata` | 用户自定义属性 |

## 示例

注册单个用户：

```php
$auth = new Auth("appKey", "Client ID", "ClientSecret");
$user = new User($auth);

$data = array(
    'username' => 'user1',
    'password' => 'user1',
    'nickname' => 'user1',
);
$user->create($data);
```

批量注册用户：

```php
$data = array(
    array('username' => 'user2', 'password' => 'user2', 'nickname' => 'user2'),
    array('username' => 'user3', 'password' => 'user3', 'nickname' => 'user3'),
);
$user->create($data);
```

## 常见问题

**中文乱码**

```php
// 纯 PHP 页面
header("Content-Type:text/html;charset=utf-8");

// HTML 混编页面
// <meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
```

**错误码说明**

SDK 直接返回 REST API 的错误码及描述，详见 [REST API 常见错误码](https://docs-im.easemob.com/im/other/errorcode/restapi)。

**使用代理**

```php
use Easemob\Auth;
use Easemob\Http\Http;

$auth = new Auth("appKey", "Client ID", "ClientSecret");
Http::setProxy("ip地址", 8080);
```

## 链接

- [GitHub 仓库](https://github.com/Easemob-Community/easemob-php-server-sdk)
- [Packagist](https://packagist.org/packages/easemob-community/easemob-php)
- [环信服务端文档](https://docs-im.easemob.com/im/server/ready/intro)
