---
layout: post
title: Bower 파일 정리하기
date: 2015-06-19 12:05:00
summary: Gulp 로 Bower file 들을 깔끔하게 정리해보아요!
categories: webpack
---

문제
-----
하나하나 bower_components/라이브러리폴더/bower.json 에서 main
필드 찾아서 concat 하고... bower 는 정말 좋은데, 사용하는 라이브러리가
많아지다보면, bower 라이브러리 파일 관리가 귀찮고 힘든작업이되요.

mainBowerFiles ([Github](https://github.com/ck86/main-bower-files))
----
정말 중요하면서, 간단한 일을 해주는 녀석이에요. bower dependencies
들을 보고, 해당 패키지에서 bower.json 안에 main 필드에 있는 녀석들을
합쳐서 리스트로 만들어줘요. 만약 해당패키지에서도 dependencies 가 있다면,
그 녀석들도 추가해주는 건 기본이죠! (진짜 좋아요 :D)

Gulp
-----
Gulp 와 main-bower-files 를 이용해서 모든 bower dependency
들을 간단하게 vendor.js 와 vendor.css 로 모아보아요.

[![asciicast](https://asciinema.org/a/083janiohu7za8dpoqr34y7aw.png)](https://asciinema.org/a/083janiohu7za8dpoqr34y7aw)

정말좋죠?
