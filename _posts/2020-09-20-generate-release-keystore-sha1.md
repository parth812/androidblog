---
layout: post
title:  "Getting Android Release Keystore SHA1 Fingerprint"
categories: Release SHA1
tags:  Release Keystore SHA1 Android
author: Parth Darji
---

* content
{:toc}

This article will introduce how to generate SHA1 for release Keystore.
This is more convenient and easy method to generate SHA1.

## Follow steps

To find out the Android SHA1 fingerprint for release keystore, follow these steps:

 - Open terminal
 - Change the directory to the JDK bin directory, mine was jdk1.7.0_05 (could be different for you).

```js
	cd C:\Program Files\Java\jdk1.7.0_05\bin
```
- Next we have to run the keytool.exe. Use the following line to get the SHA1 fingerprint.

```js
keytool -list -v -keystore {keystore_name} -alias {alias_name}
```

## Example:
```js
keytool -list -v -keystore C:\Users\MG\Desktop\test.jks -alias test
```
It will prompt for a password.
Enter the password, you will get the SHA1 and MD5 fingerprint.


![](https://i0.wp.com/www.truiton.com/wp-content/uploads/2015/04/Android-SHA1-Fingerprint-three.jpg?w=682&amp;ssl=1")

Android SHA1 Fingerprint
Extracting the SHA1 fingerprint from an Android keystore cannot be simpler than this. Above steps can be used on Windows, Mac and on Linux machines.

For Debug mode:
```js
keytool -list -v -keystore ~/.android/debug.keystore -alias androiddebugkey -storepass android -keypass android 
```



![](https://img.alicdn.com/tfs/TB16.GnOpXXXXXdapXXXXXXXXXX-307-134.png)

## Blob 对象

Blob 对象是一个字节序列。拥有 `size` 和 `type` 等属性。

拥有 2 个只读状态 `OPEND` 和 `CLOSED。`

Blob 对象属于 JavaScript Web APIs 中的 File API 规定的部分，可以参考 W3C 文档中的 [ The Blob Interface and Binary Data](https://www.w3.org/TR/2015/WD-FileAPI-20150421/#blob)

再回来看看我们的代码里是这么写的，使用了 Blob 的构造函数：

```js
var blob = new Blob([content]);
```

使用方括号的原因是，其构造函数的参数为以下4中：

- ArrayBuffer [TypedArrays] elements.
- ArrayBufferView [TypedArrays] elements.
- Blob elements.
- DOMString [WebIDL] elements.

所谓 `ArrayBuffer` 是一种用于呈现通用、固定长度的二进制数据的类型。详情可以参考 [ArrayBuffer -MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer) 以及 [ECMAScript2015 标准中的 ArrayBuffer](http://www.ecma-international.org/ecma-262/6.0/#sec-arraybuffer-objects)。

## Blob URLs

Blob URLs 被创建或注销是使用 `URL` 对象上的方法。这个 `URL` 对象被挂在 `Window` (HTML) 对象下，或者 `WorkerGlobalScope` (Web Workers)对象下。

拥有以下静态方法 `createObjectURL` 和 `revokeObjectURL`，用于创建一个 blob 对象的 url 和注销这个 blob url。

详情可查看 [关于创建和注销 Blob URL 的 W3C 标准文档]( https://www.w3.org/TR/2015/WD-FileAPI-20150421/#creating-revoking)

## 模拟 click

```js
element.click();
```

在 W3C 中很早就有这个[规范](https://www.w3.org/TR/DOM-Level-2-HTML/html.html#ID-2651361)，不需要写繁琐的模拟事件触发的代码。

## summary

目前我将这个技术使用在 天猫双十一技术和UED庆功会 的摇火箭大屏游戏中。最后的游戏结果排名，在请求了接口后，在前端直接生成并下载到了本地，作为记录保存。主要也是因为服务端暂时没有提供这个一张表去记录游戏结果，于是采用了前端记录的解决方案。

大家当时都玩的好开心啊，😁。你们的甘其食和全家卡的名单就是这样生成的！

## reference

- [在浏览器端用JS创建和下载文件 -alloyteam](http://www.alloyteam.com/2014/01/use-js-file-download/)
