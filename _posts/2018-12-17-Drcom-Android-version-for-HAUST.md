---
layout: post
title: "河南科技大学third-party上网认证客户端"
date: 2018-12-17
categories: java
tags: [java, andriod, drcom]
---

实在是忍受不了哆点的卡顿，于是从github上找到了大佬的项目，动手自己适配了一个。第一次做安卓踩了不少的坑，真是头发都白了。主要是gradle一直build falied，去CSDN看各种解决方案都没有用，后来挂上ssr,设置proxy(端口1080，SOCKS5), 结果AS下载了一个东西就编译过了真是被墙坑哭了(F**K GFW)

## project
[DrcomAndroidHAUST](https://github.com/yh-cs/DrcomAndroidHAUST)
## screenshot
![index](https://github.com/yh-cs/yh-cs.github.io/blob/master/img/Screenshot_20181217.png)
## referenced
[drcoms](https://github.com/drcoms)
[wintercoder](https://github.com/wintercoder)
[jlu-drcom-java](https://github.com/drcoms/jlu-drcom-client/tree/master/jlu-drcom-java)
## compatibility
仅支持6.0以上的设备
## details
删除
~~~
private Button btnLogout;
private void showNotification();
public void notifyLogout();
private boolean logout() throws IOException;
private byte[] makeLogoutPacket();
~~~
删除了通知栏通知，android9.0后台限制比较严格，留个通知息屏就没了，索性删除了
河科大的认证服务器地址为
~~~
210.43.0.195
~~~
河南科技大学并不需要keepAliveVer理论上打开一次退出就可以了，但并未删除相应的模块，以防别的学院需要

## restrict
安卓工程用的是 api28 只能运行再安卓系统版本6.0及以上的设备，6.0以下的话会报错。

## Bug find
发现大佬一处bug
~~~
  // 解锁WifiLock
    public void releaseWifiLock() {
        // 判断时候锁定
        if (mWifiLock.isHeld()) {
            mWifiLock.acquire();
        }
    }
~~~
这里解锁应该是 mWifiLock.release() 不太重要所以抱着不打扰的心态并没有提pr