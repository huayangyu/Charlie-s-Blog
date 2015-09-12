---
layout: post
title:  "工程所在文件夹的名字改动以及zbarSDK 64位冲突解决"
date:   2015-08-12 12:33:37
categories: Charlie update
body-class: post-welcome
---

要上线了，将文件夹的名字改了下，然后又找不到-lPods那样的问题，

1我先是删掉了setting里的 Other C Flags 里的"${PODS_ROOT}/Headers/Public/AFNetworking" 和 -isystem 之类的选项

2然后，在Edit Scheme里build 的地方加了Pods-projName，然后把它挪到了第一个 （后来成功之后我删掉了这个，也没有什么影响了）

3接着Mr.Wang说 对照自己Setting和Pods里的Build Active Only (BAO)选项是不是一样的（因为cocoapods 默认的是debug = yes， 我这边当时报错是因为工程里的BAOw中debug设置成了 No，所以就有了冲突）

4将所有的32位第三方库变成64位的，这里用的方法和07-31 firstpost 里用的是同一个办法

5在转zbarSDK的时候发现base64_encode与其他库有冲突，在网上找到办法是将zbarSDK里的symbol.c里搜索base64_encode，然后将base64_encode 改成了base64_en，重定义的冲突就解决了。