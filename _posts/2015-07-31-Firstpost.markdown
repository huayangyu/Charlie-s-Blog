---
layout: post
title:  This is my first post
date:   2015-07-31 13:04:10
categories: Charlie update
body-class: post-welcome
---

Hello,guys and girls!

我的项目从SVN上checkout出来的，之前该项目有用过pods，导入了一个2.0版本的AFNetworking和Reachability，checkout项目之后，就想用继续用pods，可每次podsinstall之后都会有一大堆警告和错误
。error提示是找不到-lAFNetworking 还有 i386的字样，昨晚小悦用iPhone 4s 做了下试验，发现能用，5s就报错。早上来公司，决定试试看能不能把所有的pods转成64位支持的，于是重写了下podfile文件。

   platform :ios, '7.0'
  
   target 'QiaoGuShop' do
   pod 'AFNetworking', '~> 2.5.4'
   pod 'Reachability', '~> 3.2'
   end
  
  
   post_install do |installer|
      puts 'Updating project to 64 Bit'
      installer.pods_project.targets.each do |target|
          target.build_configurations.each do |config|
              config.build_settings['ARCHS'] = "$(ARCHS_STANDARD_INCLUDING_64_BIT)"
          end
      end
  end

这个hook是来自
<a href="https://gist.github.com/funroll/7faf18b4972d72cd284e"></a>

链接里的hook中installer.project.targets.each do |target| 的地方改成 install.pods_project.targets.each do |target|	不然会报错

这个建议是由segiddins提供的

<a href="http://stackoverflow.com/questions/28343242/how-to-convert-xcode-32-bit-app-into-64-bit-xcode-app">另外确保工程支持32位和64位</a>
