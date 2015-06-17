---
layout: post
title: Browserify 소개
date: 2015-05-25 18:05:09
summary: 프론트엔드 코드를 깔끔하게 정리해보아요.
categories: browserify
---

안녕하세요! 오늘은 Javascript 코드를 깔쌈하게 빌드하는 방법에 대해서 얘기해 보려고 해요.
[Browserify](https://github.com/substack/node-browserify) 는
Node.js 기반 javascript code 를 브라우저 환경에서도 실행 가능하도록 만들어주는 녀석이에요.<br/>
예를 들자면,

{% highlight javascript %}
var path = require('path');
var foo = require('./helpers/foo')

// Some codes..

module.exports = function bar () {
  return 'bar'
};
{% endhighlight %}

이런 코드도 브라우저에서도 실행 가능하도록 만들어줘요.

반대로 생각해보자면 __browser 에서 실행되는 코드를 node 스타일로__ 짤 수 있도록 해준다는거죠.<br/>
이건 정말 큰 장점인데 기존의 [AMD](https://github.com/amdjs/amdjs-api/blob/master/AMD.md) 방식을 사용하게 되면, 코드를 AMD 스타일로 짜야 한다는 단점이 있어요.<br/>

{% highlight javascript %}
define("alpha", ["require", "exports", "beta"],
  function (require, exports, beta) {
    exports.verb = function() {
      return beta.verb();
      //Or:
      return require("beta").verb();
    }
  }
);
{% endhighlight %}

이런 식으로요.<br/>

하지만 __Browserify__ 는 __Node.js__ 의 [Module API](https://nodejs.org/api/modules.html) 를 그대로 사용하기 때문에, 일단 node 코드로 작성하고 나중에 browserify 로 컴파일만 해주면
node 와 browser 환경에서 둘다 실행되요. <br/>
또 끝내주는 특징 중 하나는, node 기반 package 를 그대로 사용할 수 있다는 부분이에요.
[built-in package](https://github.com/substack/node-browserify#compatibility) 들은 물론이고,
[npm](https://www.npmjs.com/) 으로 설치한 package 모두 컴파일을 통해 브라우저에서도 그대로 사용할 수 있어요.
{% highlight javascript %}
var path = require('path');
var _ = require('underscore')
var foo = require('./foo')
{% endhighlight %}
__이런 코드를 브라우저에서도 그대로 쓸 수 있다는거에요! 얏호!!__ <br/>

[Bower](http://bower.io/) 에서 받은 외부 라이브러리들도 [browserify-shim](https://github.com/thlorenz/browserify-shim) 플러그인을 사용해서 그대로 사용할 수 있구요.

{% highlight javascript %}
// package.json
// ...
"browserify": {
  "transform": ["browserify-shim"]
},
"browserify-shim": {
  "jquery": "global:$"
}
// ...
{% endhighlight %}

이런식으로요.

standalone, external 등 여러가지 옵션을 사용해서 라이브러리화 & 최적화도 가능해요!

[Webpack](http://webpack.github.io/) 이라는 녀석도 있는데 이친구는 다음번에 알아보도록 해요.
