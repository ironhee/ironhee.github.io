---
layout: post
title: Webpack - 모듈화와 속도를 모두 잡는 방법.
date: 2015-06-17 18:05:09
summary: Browserify 빌드가 느리다고요? 그렇다면 Webpack을 씁시다.
categories: webpack
---

안녕하세요! 이번에 소개할 녀석은 [Webpack](http://webpack.github.io/) 이라는 녀석이에요.

Browserify 의 문제점
-----
[Browserify](/browserify/2015/05/26/browserify-introduce/) 를
사용하다보면 처음에는 빌드 속도가 조금 있긴하지만, 개발에는 크게 지장이 생기지 않아요.
하지만, 소스코드가 많아지면 많아질수록 참기 힘들정도로 느려져요.
보통 browserify 를 사용하게 되면 watch 를 하게되는데 한번 소스변경하고 10초동안
멍때리고 다시 코딩하고 그러면 흐름이 끊어지죠...

저같은 경우는 처음에는 빌드에 2초가 걸리다가 나중에는 한번 변경사항이 생겨서
소스코드를 수정하면 빌드에 20초까지 걸리더라구요.

그래서 browserify 빌드 속도를 개선하기위해서, 소스코드 길이도 줄여보고,
[watchify](https://github.com/substack/watchify) 도 사용해보았지만 의미있는 단위로 속도가 빨라지지 않았어요.

Webpack?!!!
---------
그러다가 webpack 도 [Node Module API](https://nodejs.org/api/modules.html)를 그대로 사용하고, browserify에서 변경도 쉽고 빌드 속도도 훨씬 빠르다는걸 알게 되었어요.

그래서 browserify 에서 webpack 으로 변경했어요.

이럴수가... 초기 빌드는 20초에서
10초로, watch 중에서의 빌드는 20초에서 0.1~3 초 정도로 아주 크게 줄어들었어요.
([cache](http://webpack.github.io/docs/configuration.html#cache)) ???!!! __얏호!__

마이그레이션도, 문서화가 잘 되어있어서 어렵지 않았어요. ([링크](http://webpack.github.io/docs/webpack-for-browserify-users.html))

Webpack 을 사용하시게된다면, [babel-loader](https://github.com/babel/babel-loader) 를 사용해서 ES6로 코드를 작성하시는걸 추천해요.
[Airbnb - Javascript Style Guide](https://github.com/airbnb/javascript)도 벌써 ES6 기준으로 바뀌었더라구요.

또, 개발환경에서는 [sourcemap option](http://webpack.github.io/docs/configuration.html#devtool) 도 잊지않고 켜두시구요! 컴파일된 소스로 디버깅을 하면
현기증이나요.

결과
-----
- 현재 [libraryTarget](http://webpack.github.io/docs/configuration.html#output-librarytarget) 옵션을 'umd' 로 설정해서 한 소스로,
npm (node.js 환경) 과 bower (browser 환경) 두 환경에서 공용으로
사용할 수 있는 결과물 코드를 만들어내고 있어요.
- babel-loader 를 사용해서 ES6 로 모든 코드를 작성하고 있구요.
- 빌드속도는 초기빌드 후에 0.1~3초 밖에 걸리지 않아요.
- 물론 모든 코드는 node module style 로 모듈화가 되어있구요.

안 쓸 이유가 있나요? Webpack은 사랑입니다 :D

예시
------
{% highlight javascript %}
// webpack.config.js
'use strict';


module.exports = {
  devtool: "eval",
  resolve: {
    modulesDirectories: ['src/js'],
    extensions: ['', '.es6', '.js']
  },
  entry: {
    'main': './src/js/main.es6'
  },
  output: {
    path: 'dist/js/',
    filename: 'main.js'
  },
  externals: {
    'jquery': '$',
    'underscore': '_',
    'react': 'React'
  },
  module: {
    loaders: [
      { test: /\.es6$/, loader: 'babel-loader' }
    ]
  }
};
{% endhighlight %}

요렇게 Webpack 설정파일을 만들고,

{% highlight bash %}
webpack
{% endhighlight %}

으로 한번 빌드하거나,

{% highlight bash %}
webpack --watch
{% endhighlight %}

로 소스코드를 스토킹하게 할 수 있어요.

gulp 를 사용하고 계신분들은 [여기](http://webpack.github.io/docs/usage-with-gulp.html)를 참고하세요!


추천링크
-----
- [Browserify VS Webpack - JS Drama](http://blog.namangoel.com/browserify-vs-webpack-js-drama)
