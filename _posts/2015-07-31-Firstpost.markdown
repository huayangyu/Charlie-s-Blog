---
layout: post
title:  This is my first post
date:   2015-07-31 13:04:10
categories: Charlie update
body-class: post-welcome
---

Hello,guys and girls!


我的项目从SVN上checkout出来的，之前该项目有用过pods，导入了一个2.0版本的AFNetworking和Reachability，checkout项目之后，就想用继续用pods，可每次podsinstall之后都会有一大堆警告和错误
。error提示是找不到-lAFNetworking，昨晚小悦用iPhone 4s 做了下试验，发现能用，5s就报错。早上来公司，决定试试看能不能把所有的pods转成64位支持的，于是重写了下podfile文件。


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


链接里的hook中"installer.project.targets.each do |target|" 的地方改成 "install.pods_project.targets.each do |target|"不然会报错
这个建议是由segiddins提供的

<a href="https://gist.github.com/funroll/7faf18b4972d72cd284e">hook</a>

如果还是不行，肯能是因为工程的valid architecture的问题，正在研究中,continuing...

继续更新，第二回被pods整了，公司用的是SVN，我以前用的是Git，不懂怎么merge；因为以前git 可以branch -d 一个出来，所以做实验的时候也就不怕会影响到原来的代码，目前还不敢用svn直接来尝试，前几天搭建了一下午的gitHub，没成~。继续回到pods的问题，经历过两次坑，现在碰到git install 之后的问题，比如 not found -lPods 之类的，都采用一个办法去解决了----> 就是删掉所有和cocoa pods 有关的，podfile看你自己情况决定要不要保留，然后就老实得重新init，install吧，总会成功的。



      platform :ios, '7.0'

      target 'QiaoGuShop' do  
      pod 'Masonry', '~> 0.6.2'
      pod 'Reachability', '~> 3.2'

      source 'https://github.com/CocoaPods/Specs.git'
      pod 'AFNetworking', '~> 2.5.4'
      pod 'libqrencode', '~> 3.4.2'
      pod 'XMLReader-Arc', '~> 1.1'
      pod 'OpenSSL', '~> 1.0.203'

      end


   上面source的地方高能预警。。。。



