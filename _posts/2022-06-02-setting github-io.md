---
layout: post
title: setting github.io local server for mac
categories: study
tags: [study]
---

## 1. github.io git repository 생성
new repository 생성하고 앞에 username 을 붙여야 한다.   
내 username 은 hyuzni로 되어있으므로,   
hyuzni.github.io로 repository 생성.  
블로그 답게 public 선택하고 readme 파일은 자유.   

## 2. 페이지를 local에서 띄우기 위한 bundler 설치

# ruby 의 패키지 매니져인 gem 설치
터미널에 gem이라고 쳤을 때 'RubyGems is a sophisticated package manager for Ruby.'   
요렇게 뜨는것이 나는 이미 설치가 되어있던거 같다. 왠지는 모름   
그래서 gem을 통해 bundler, jekyll 설치하려니 아래 문구의 에러 발생    
'You don't have write permissions for the /Library/Ruby/Gems/2.6.0 directory.'   
permissions가 들어가는거 보니 권한문제 인듯 하다.   

구글링 결과 rbenv 를 통해 처리를 해줘야 한다고 하니 이게 뭔지 찾아본다.   
rbenv는 루비의 버전을 독립적으로 사용할 수 있도록 도와주는 패키지? 라는데 그래도 뭔지 모르겠다.   
여기서 알게된 점은 mac에서 쓰는 homebrew 가 ruby 언어 기반이라는 것이다.   
그래서 기본적으로 ruby가 설치되어 있고? 나는 gem을 설치 없이 쓸 수 있었나보다. 아님말고;   

다시 문제해결로.   
brew를 업데이트 해주고 rbenv를 설치한다.   
{% highlight zsh %}
brew update
brew install rbenv ruby-build
{% endhighlight %}

뒤에 ruby-build는 뭐 설치 후 빌드를 하라는건가? 모름 일단 따라함.   
잘 설치가 되었는지 버전 확인 하고 rbenv로 관리되는 ruby를 설치하기 위해 설치할 수 있는 ruby 버전을 확인한다   
{% highlight zsh %}
rbenv versions
rbenv install -l
{% endhighlight %}

출력물은 아래와 같다.   

2.6.10   
2.7.6   
3.0.4   
3.1.2   
jruby-9.3.4.0   
mruby-3.0.0   
rbx-5.0   
truffleruby-22.1.0   
truffleruby+graalvm-22.1.0   

나는 최신버전인 2.6.10을 선택함.   
{% highlight zsh %}
rbenv install 2.6.10
{% endhighlight %}

rbenv 로 global 버전을 방금 다운받은 버전으로 변경하고,   
쉘 설정파일을 열어 환경변수를 추가하기 위해 아래의 코드를 추가한다.   
{% highlight zsh %}
rbenv global 2.6.10 // 글로벌 버전 변경   
vim ~/.zshrc // zsh 쉘 설정파일 수정   
{% endhighlight %}

zsh 쉘 설정파일에 아래 문구 추가   
{% highlight vim %}
[[ -d ~/.rbenv ]] && \
  export PATH=${HOME}/.rvenv/bin:${PATH} && \
  eval "$(rbenv init -)"
{% endhighlight %}

source로 코드를 적용하고 다시 설치를 해보자   
{% highlight zsh %}
source ~/.zshrc 

gem install bundler jekyll // jekyll도 같이 설치   
{% endhighlight %}

드디어 설치 성공   

## 3. bundle 로 jekyll 실행

github으로 만든 repository 경로로 이동해서 bundle 실행   
{% highlight zsh %}
bundle init
bundle add jekyll
{% endhighlight %}

이제 서버 구동 명령어만 입력하면 끝.!   
{% highlight zsh %}
bundle exec jekyll serve
{% endhighlight %}

'Server address: http://127.0.0.1:4000/'    
라고 뜨면 위 url접속해서 확인 가능하다.   

jekyll 레이아웃 테마는 어떻게 가져왔드라 ...그냥 깃헙으로 다운받아서 썻었낳ㅎㅎㅎ   
이것도 뭐 마음 급해지면 포스팅 한번 해봐야지   

오늘은 끝!   