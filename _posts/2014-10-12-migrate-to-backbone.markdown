---
layout: post
title: Backbone.js 도입 후기
date: 2014-10-12 22:10:32
summary: MV* 프레임워크 Backbone.js 를 도입해보았어요.
categories: Backbone
---
##Backbone.js 쓰게 된 이유

<div style="text-align: center">
    <img src="http://beageek.biz/wp-content/uploads/backbone-js.gif" alt="Backbone" style="width: 100%; height: auto;">
</div>
<br>

1. 프론트엔드 코드는 많이 복잡하고 알기 힘들어졌는데 기획과 요구사항이 많이 바뀌게 되었어요.

<div style="text-align: center">
    <img src="http://tech.co/wp-content/uploads/2012/10/Pivots.jpeg" alt="pivoting" style="height: 200px; width: auto;">
</div>
<br>

2. 코드의 중복와 직접 만든 코드구조(MVC) 등으로 소스를 변경/ 관리하기가 매우 힘들었어요. ([DRY](http://en.wikipedia.org/wiki/Don't_repeat_yourself) 법칙에 어긋남)
3. MVC 관련 패턴 (MVVM, MV*) 프레임 워크로 보통 [Angular.js](https://www.angularjs.org/)와 [Backbone.js](http://backbonejs.org/)를 많이쓰더라구요.


<div style="text-align: center">
    <img src="https://pbs.twimg.com/profile_images/2149314222/square.png" alt="Angular.js" style="height: 200px; width: auto;">
    <img src="http://beageek.biz/wp-content/uploads/backbone-js.gif" alt="Backbone.js" style="height: 200px; width: auto;">
</div>
<br>


4. Backbone.js 와 Angular.js 공식 홈페이지와 [Angular.js or Backbon.js](http://stackoverflow.com/questions/14505016/angularjs-or-backbone-js) 를 읽어보았어요.
5. Angular.js는 처음부터 권장 스타일로 개발해야하는데 Angular 스타일로 소스를 바꾸는건 너무 비용이 크다고 생각했어요.
6. Backbone.js는 가볍고 프로젝트에 바로 적용시킬 수 있을 정도로 유연성도 있어서 금방 도입이 가능할 것 같았어요.

##Backbone.js을 도입하면서
1. 기존 View 와 Controller 로직을 Backbone.js View 를 사용하여 바꾸었어요.
2. View 로직을 [Handlebars](http://handlebarsjs.com/) (Template engine)가 처리하게 되었어요. 템플릿을 따로 관리할 수 있게 되었죠.

{% highlight javascript %}

// 기존의 코드
var MyView = function (model) {
    var $el = ...;

    var createHTML = function () {
        var html = '<div class="some-class">' +
            model.someValue + '</div>';
        return html;
    }

    this.render = function () {
        this.$el.html(createHTML());
    }
}

// Backbone 을 사용하여 바뀐 코드
var handlebarTemplate = ... // load handlebar template

var MyView = new Backbone.View.extend({
    className: 'some-class',
    template: Handlebars.complie(handlebarTemplate),
    render: function () {
        var html = this.template(this.model.toJSON());
        this.$el.html(html);
    }
});
{% endhighlight %}

4. HTML 에 의존하던 소스코드를 리펙토링하여 Backbone.js Model 을 사용하도록 만들었어요.

##얻게된 장점
1. MVC 자체를 제작 / 유지보수하는 비용이 사라져 비즈니스 로직에 집중할 수 있게 되었어요.
2. REST API 에 맞게 프론트엔드 코드로 구현하기가 쉬워졌어요.
3. Model, View, Template 로 책임을 알맞게 분리하였기 때문에 코드가 간결해지고 단단해졌어요.
4. Backbone.js 가 내부적으로 [underscore.js](http://underscorejs.org/) 를 사용하는데 이게 정말정말 좋아요.
5. 그래서 코딩이 더 재미있어졌어요.

###이런 분들에게 추천해요.
1. [Django](https://www.djangoproject.com/) 보다 [Flask](http://flask.pocoo.org/) 를 선호하시는 분
2. 기존에 진행중이던 프로젝트에 MVC 계열 프레임워크를 도입하고 싶으신분
3. REST API 에 맞게 프론트엔드 코드를 작성하고 싶으신분
4. underscore.js 를 사랑하시는 분
