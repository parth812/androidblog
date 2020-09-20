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

```java
	cd C:\Program Files\Java\jdk1.7.0_05\bin
```
- Next we have to run the keytool.exe. Use the following line to get the SHA1 fingerprint.

```java
keytool -list -v -keystore {keystore_name} -alias {alias_name}
```

## Example:
```java
keytool -list -v -keystore C:\Users\MG\Desktop\test.jks -alias test
```
It will prompt for a password.
Enter the password, you will get the SHA1 and MD5 fingerprint.


![](https://i0.wp.com/www.truiton.com/wp-content/uploads/2015/04/Android-SHA1-Fingerprint-three.jpg?w=682&amp;ssl=1")

Android SHA1 Fingerprint
Extracting the SHA1 fingerprint from an Android keystore cannot be simpler than this. Above steps can be used on Windows, Mac and on Linux machines.

For Debug mode:
```java
keytool -list -v -keystore ~/.android/debug.keystore -alias androiddebugkey -storepass android -keypass android 
```

