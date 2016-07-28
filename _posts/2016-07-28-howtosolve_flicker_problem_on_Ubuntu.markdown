---
layout: single
title: 우분투에서 Nvidia GPU 드라이버 업데이트 후 UI Flickering 문제 해결
category:
 - Linux
tags:
 - Flickering
 - Nvidia GPU driver
 - Linux
 - Ubuntu
summary: 우분투 환경에서 NVIDIA GPU 드라이버 업데이트 후 발생하는 화면 깜빡임(Flickering) 문제 해결
---

우분투 14.04 환경에서 Nvidia GPU 드라이버를 업데이트 하고 나면, 마우스를 움직일 때마다 데스크탑 화면의 UI의 일부 색이 깜빡이는 현상이 생긴다. 그냥 깜빡이는 문제만 발생하면 무시하겠는데(어차피 작업은 주로 쉘환경에서만 하니..) 문제는 XMDB로 영화를 볼 때 화면의 색이 계속 깜빡여서 도저히 참고 볼수가 없는 것이다. 

첨에는 이 문제의 원인이 새로 업데이트한 NVIDIA GPU 드라이버 자체의 문제인 걸로 생각하고, 이전 버전의 드라이버를 여러개 받아서 깔아봤으나, 이 문제의 현상이 해결되지 않았다. 해결책을 구글링하던 중, 드라이버 업데이트시 문제가 발생 할 때 Xorg 라이브러리도 다시 깔면 많은 문제(?)가 해결된다는 글을 보고, 혹시나 해서 다시 설치 해봤더니 빙고! 깜빡임 현상이 없어졌다.



>Reinstalling Xorg also helps in other cases:
>Remove existing xorg using the following command
`sudo apt-get remove --purge xserver-xorg`
>Install xorg using the following command
`sudo apt-get install xserver-xorg`
>Reconfigure xorg using the following command
`sudo dpkg-reconfigure xserver-xorg`
>After this it is recommended to reinstall the video driver if you are using Nvidia or Ati as mentioned above.


위와 같이 Xorg를 재설치 하고, Nvidia 드라이버는 그대로 둔 채 PC를 리부팅 하니 문제가 해결됐다. -끝-
