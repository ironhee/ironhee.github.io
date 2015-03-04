---
layout: post
title: Sinon.js FakeServer
date: 2015-03-04 17:03:03
summary: Sinon.js FakeServer를 이용해서 XHR 포함된 코드를 간단하게 테스트 해보아요.
categories:
---

## Sinon.js?

자바스크립트를 위한 [Spy](http://sinonjs.org/docs/#spies), [Stub](http://sinonjs.org/docs/#stubs), [Mock](http://sinonjs.org/docs/#mocks) 를 제공하는 라이브러리에요.<br/>
보통 [Mocha](https://github.com/mochajs/mocha), [Chai](https://github.com/chaijs/chai) 등 테스팅 프레임워크들과 함께 쓰이구요!<br/>

### XHR 테스팅의 어려움

 기존의 Javascript 코드에서 단어를 세는 함수라던가, 문자열을 비교하는 함수같은 경우는 Mocha와,
Chai를 조합해서 간단하게 테스팅을 할 수 있었어요.<br/>


{% highlight javascript %}
/* 구현 */
var coutWord = function (str) {
  var wordCount = 0;
  // 어쩌구 저쩌구...
  return wordCount;
};

/* 테스트 */
describe('coutWord', function () {
  it('shoud countWord correctly', function () {
    expect(countWord('foo bar')).to.equal(2);
  });
});
{% endhighlight %}

 하지만 서버로 XHR (XMLHttpRequest)작업이 있는 코드는 기존 방법만으로는 테스팅하기 힘들었어요.

{% highlight javascript %}
/* 구현 */
var user = null;

var signin = function (email, password) {
  $.ajax('/auth/signin/', {
      // 어쩌구 저쩌구...
      type: 'post'
    })
    .done(function () {
      // 무언가 멋진 일을 해요
    })
    .fail(function () {
      // 에러를 처리해요
    });
}

var getUser = function () {
  return user;
};

/* 테스트 */
describe('signin', function () {
  it('shoud load user from server', function (done) {
    // 음... 여기서 자꾸 막혀요...
    signin('test@gmail.com', 'foobar')
      .then(function () {
        expect(getUser().email).to.equal('test@gmail.com');
        done();
      });
  });
});
{% endhighlight %}
요런코드요...

### FakeXMLHttpRequest & FakeServer

Sinon.js 는 [XMLHttpRequest](https://developer.mozilla.org/ko/docs/XMLHttpRequest) 의 가짜 구현을 제공해요.
서버에 요청(Request)을 하고 서버가 실제로 응답(Response)을 해주는 것 같지만, Sinon.js 가 서버 역할을 해준다는거죠. <br/>
그 기능에 대해 [FakeXMLHttpRequest]() 라는 API를 제공하는데, 저는 더 고차원적으로 추상화된 FakeServer 라는 API 를 사용했어요. 편하거든요!

#### FakeServer를 이용한 테스팅

{% highlight javascript %}
describe('signin', function () {

  it('shoud load user from server', function (done) {
    var server = sinon.fakeServer.create();
    server.autoRespond = true;

    // 미리 정한 규칙에 맞아 떨어지는 Request에게 정의된 Response 를 넘겨줘요.
    server.respondWith("POST", '/auth/signin/', [
      200,
      {
        "Content-Type": "application/json"
      },
      JSON.stringify({
        id: 1,
        username: 'Ironhee'
      })
    ]);

    // 오!! 이제 잘되요!
    signin('test@gmail.com', 'foobar')
      .then(function () {
        expect(getUser().email).to.equal('test@gmail.com');
        done();
      });

    server.restore();
  });
});
{% endhighlight %}
결국 이런식으로 해서 XHR 테스팅을 할 수 있었고, 테스팅도 빠르게 할 수 있어서 만족하고 있어요!

참고링크
---
- __Mocha.js__: simple, flexible, fun javascript test framework for node.js & the browser. (BDD, TDD, QUnit styles via interfaces)
  + [Github](https://github.com/mochajs/mocha)
  + [Document](http://mochajs.org)
- __Chai.js__: BDD / TDD assertion framework for node.js and the browser that can be paired with any testing framework.
  + [Github](https://github.com/chaijs/chai)
  + [Document](http://chaijs.com)
- __Sinon.js__: Test spies, stubs and mocks for JavaScript.
  + [Github](http://sinonjs.org/)
  + [Document](http://sinonjs.org/)


