---
layout: post
title: Sublime Text 2, Dropbox 로 동기화시키기
date: 2014-10-11 00:10:53
summary: Sublime Text 2 세팅과 패키지를 Dropbox 로 동기화시켜보아요
categories: SublimeText2 Dropbox
---

여러 Mac/PC 에서 SublimeText를 사용할 경우 Sublime Text 2 세팅과 패키지를 Dropbox로 연동시키면 매번 세팅과 패키지를 다시 세팅하고 설치할 필요 없어서 편리해요.

###Sublime Text 2 세팅/패키지를 DropBox로 동기화 시켜보아요

1. 먼저 Sublime Text 2 디렉토리에 접근해요.

        cd ~/Library/Application\ Support/Sublime\ Text\ 2/

2. 기존 Sublime Text 2 세팅/패키지를 DropBox 폴더로 옮겨요.

        mkdir ~/Dropbox/Some-Path
        mv Installed\ Packages ~/Dropbox/Some-Path/Installed\ Packages
        mv Packages ~/Dropbox/Some-Path/Packages
        mv Pristine\ Packages ~/Dropbox/Some-Path/Pristine\ Packages

3. 원래 Sublime Text 2 디렉토리에 방금 드랍박스로 옮긴 폴더에 대한 심볼릭 싱크를 만들어요.

        ln -s ~/Dropbox/appdata/sublime/Installed\ Packages ./Installed\ Packages
        ln -s ~/Dropbox/appdata/sublime/Packages ./Packages
        ln -s ~/Dropbox/appdata/sublime/Pristine\ Packages ./Pristine\ Packages

4. 완성되었어요!
5. 이제 다른 Mac/PC 에서 3번부터 따라하면 Sublime Text 2 세팅과 패키지가 동기화되요. 얏호!
