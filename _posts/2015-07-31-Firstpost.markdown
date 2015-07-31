---
layout: post
title:  This is my first post
date:   2015-07-31 13:04:10
categories: jekyll update
---

Hello,guys and girls!

我的项目从SVN上checkout出来的，之前该项目有用过pods，导入了一个2.0版本的AFNetworking和Reachability，checkout项目之后，就想用继续用pods，可每次podsinstall之后都会有一大堆警告和错误
。error提示是找不到-lAFNetworking 还有 i386的字样，昨晚小悦用iPhone 4s 做了下试验，发现能用，5s就报错。早上来公司，决定试试看能不能把所有的pods转成64位支持的，于是重写了下podfile文件。

  1 platform :ios, '7.0'
  2
  3 target 'QiaoGuShop' do
  4 pod 'AFNetworking', '~> 2.5.4'
  5 pod 'Reachability', '~> 3.2'
  6 end
  7
  8
  9 post_install do |installer|
 10     puts 'Updating project to 64 Bit'
 11     installer.pods_project.targets.each do |target|
 12         target.build_configurations.each do |config|
 13             config.build_settings['ARCHS'] = "$(ARCHS_STANDARD_INCLUDING_64_BIT)"
 14         end
 15     end
 16 end

这个hook是来自

https://gist.github.com/funroll/7faf18b4972d72cd284e

链接里的hook中installer.project.targets.each do |target| 的地方改成 install.pods_project.targets.each do |target|	不然会报错

这个建议是由segiddins提供的

