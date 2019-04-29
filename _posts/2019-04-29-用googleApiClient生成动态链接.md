---
layout: post
author: eature
published: true
categories: other
tags:
- googleapi
- 动态链接
---

#### 什么是google动态链接
  google的动态链接可用于追踪用户的下载， 打开行为， 即当用户点链接打开或者下载app的时候， google会有回调， 让你能追踪到用户是点哪个链接下载安装或者打开的， 支持android和ios平台， 内部具体的实现原理未知
#### 怎么生成
  google提供客户端生成动态链接或者服务端生成动态链接， 各种生成方式参考[firebase文档](https://firebase.google.com/docs), 这边讲怎么用服务端生成firebase动态链接  
    1. 找到相应语言的apiClient, 可在[google官网](https://developers.google.com/api-client-library/)或者[github](https://github.com/googleapis)上找到对应的sdk， 如PHP， 找到对应的库`google-api-php-client`, 参考README安装类库， 以下以PHPClient作为例子  
    2. 先上代码  
```
<?php
/*
 | ------------------------------
 | User: Zoueature
 | Date: 2019/4/26
 | Time: 15:29
 | ------------------------------
 */

require_once './vendor/autoload.php';

putenv('GOOGLE_APPLICATION_CREDENTIALS=/path/to/servive.credentials.json');//服务账号密码的json文件
$client = new Google_Client();
$client->useApplicationDefaultCredentials();
$client->addScope('https://www.googleapis.com/auth/firebase');

$androidInfo = new Google_Service_FirebaseDynamicLinks_AndroidInfo();
$androidInfo->setAndroidPackageName('packageName');

$iosInfo = new Google_Service_FirebaseDynamicLinks_IosInfo();
$iosInfo->setIosAppStoreId('applestoreId');
$iosInfo->setIosBundleId('bundleId');
$iosInfo->setIosCustomScheme('schema');

$linkInfo = new Google_Service_FirebaseDynamicLinks_DynamicLinkInfo();
$linkInfo->setLink('the origin link);
$linkInfo->setDomainUriPrefix('https://example.page.link');

$linkInfo->setAndroidInfo($androidInfo);
$linkInfo->setIosInfo($iosInfo);

$creator = new Google_Service_FirebaseDynamicLinks($client);
$request = new Google_Service_FirebaseDynamicLinks_CreateShortDynamicLinkRequest();
$request->setDynamicLinkInfo($linkInfo);
$res = $creator->shortLinks->create($request);
$shortLink = $res->getShortLink();
echo $shortLink;
```    
3. 创建google client  
4. 设置必要的android包和ios包信息， android包的packageName为必填项， ios的appleStoreId和bundleId为必填项  
5. 创建动态链接的类， 填充android和ios的包信息  
6. 创建api请求类， 生成动态链接  
7. done