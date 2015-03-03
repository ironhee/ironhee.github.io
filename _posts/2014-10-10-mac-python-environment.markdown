---
layout: post
title: 맥에 파이썬 개발환경 세팅하기
date: 2014-10-10 23:10:40
summary: HomeBrew 를 써서 Mac에 Python2.7 개발환경을 만들어보아요
categories: Mac Python Environment
---

1. 기존 Mac에 내장된 Python2.7 버전을 제거해요.

{% highlight bash %}
sudo rm -rf "/Library/Frameworks/Python.framework/Versions/2.7"
{% endhighlight %}

2. Python 2.7 Application 디렉토리를 제거해요.

{% highlight bash %}
sudo rm -rf "/Applications/Python 2.7"
{% endhighlight %}

3. '/usr/local/bin' 안에 있는 파이썬 2.7 버전을 가르키는 심볼릭 링크들을 제거해요.

{% highlight bash %}
ls -l /usr/local/bin | grep "../Library/Frameworks/Python.framework/Versions/2.7" | xargs rm
{% endhighlight %}

4. [Homebrew](http://brew.sh/) 설치해요! Homebrew 만세!

{% highlight bash %}
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
{% endhighlight %}

5. home-brew 의사선생님께 내 컴퓨터를 진단받아요.

{% highlight bash %}
brew doctor
{% endhighlight %}

6. '/etc/paths' 를 열어요

{% highlight bash %}
sudo vi /etc/paths
{% endhighlight %}

7. 우선순위를 바꿔요! (위쪽으로 갈수록 우선순위가 높아져요.):

{% highlight bash %}
/usr/local/bin  # 이부분이 위에 오도록 설정해요
/usr/local/sbin # 이부분이 위에 오도록 설정해요
/usr/bin
/bin
/usr/sbin
/sbin
{% endhighlight %}

8. homebrew로 파이썬을 설치해요.

{% highlight bash %}
brew install python
{% endhighlight %}

9. virtualenv를 설치해요! (시스템에 설치된 파이썬에 영향을 주지 않고 파이썬의 가상 환경을 유지할 수 있도록 도와주는 친구에요.)

{% highlight bash %}
pip install virtualenv
{% endhighlight %}

10. virtualenvwrapper 설치 (virtualenv를 더 편하게 쓸 수 있도록 도와주는 친구에요.)

{% highlight bash %}
pip install virtualenvwrapper
{% endhighlight %}

11. ~/.bash_profile 에 virtualenvwrapper 를 위한 코드를 추가해요!

{% highlight bash %}
# virtualenvwrapper를 위한 코드야!
source .virtualenvwrapper.sh
{% endhighlight %}

12. (이건 해도되고 안해도되요) mysql를 설치해요.

{% highlight bash %}
 brew install mysql
{% endhighlight %}
