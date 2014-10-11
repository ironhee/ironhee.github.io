---
layout: post
title: Ediket Backbone & Requirejs 테스팅 환경 구축하기
date: 2014-09-30 12:29:00
summary: Ediket Backbone & Requirejs Testing
categories: Ediket
---

에디켓 사이트를 개편하면서 프론트엔드 테스트 케이스가 없어서 생기는 문제점들이 많아졌어요.

개발할때는
------------
1. 소스는 복잡해지는데 테스트 케이스가 없어서 배포할 때 마다 직접 테스트를 해야해요.
2. 그러다보니 리펙토링이 너무 힘들어요...
3. 배포도 힘들죠...

그래서 테스팅 프레임워크들을 찾아봐도, Require.js 와 Backbone.js로
구성된 Ediket 사이트에서는 바로 적용하기가 힘든 것들이 많았어요...

왜 바로 적용하기 힘드냐면요
-----------------------------
1. [Backbone.js Model auto sync](http://backbonejs.org/#Model)도 있구요
2. Require.js 를 사용해서 함수와 객체들을 정의했기 때문에 테스팅 환경(node)에서 기존 요소들을 이용하기가 어려웠어요.

그러면 어떤 조합으로 테스트를 해야할까요?
-----------------------------
1. Web Ui Test
    - [Casper.js](http://casperjs.org/):
    CasperJS is an open source navigation scripting & testing utility written in Javascript for the [PhantomJS](http://phantomjs.org/) WebKit headless browser and [SlimerJS](http://slimerjs.org/) (Gecko).
    - [PhantomJS](http://phantomjs.org/):
        PhantomJS is a headless WebKit scriptable with a JavaScript API.
2. Model Test
    - [Jasmine](http://jasmine.github.io/):
        자바스크립트 코드 테스트를 위한 BDD(Behavior-Driven Development) 개발 프레임워크
    - [Sinon](http://sinonjs.org/):
        자바스크립트를 위한 독립적인 테스팅 spies, stubs 과 mocks을 제공한다.
        의존성이 없어, 다른 어떤 유닛 테스팅 프레임워크와도 잘 동작한다.

이 자료들을 참고했어요
-----------------------------
1. [node 환경에서 require.js syntax로 정의된 요소들 사용하기](http://requirejs.org/docs/node.html)
2. [Testing Backbone application with Jasmine and Sinon](http://tinnedfruit.com/2011/03/03/testing-backbone-apps-with-jasmine-sinon.html)
3. [Web UI Testing automation](http://www.slideshare.net/CreamTec/ui-testing-automation-17208623)
4. [Automated Web Testing using JavaScript by Simon Guest](http://www.slideshare.net/simonguest/automated-web-testing-using-javascript)
5. [Effective Unit Testing With Amd](http://bocoup.com/weblog/effective-unit-testing-with-amd/)

