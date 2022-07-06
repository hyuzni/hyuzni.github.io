---
layout: post
title: jenkins build permission error
categories: study
tags: [study]
---

## 1. vue-cli-service build permission error

젠킨스로 프로젝트를 빌드 할 때 권한 에러가 발생하는데,
원인은 개발서버에(ubuntu) npm 설치를 sudo로 해서 root만 접근되게끔 설정이 되어있어 젠킨스는 접근 권한이 없다고 한다.
실제로 터미널로 접근해서 root계정으로 빌드하면 잘 됨

> 아래는 npmjs 공식 문서.

[vue-cli-service build permission error](https://docs.npmjs.com/resolving-eacces-permissions-errors-when-installing-packages-globally)
  
나같은 경우는 위 문서의 5번까지만 따라하면 될 것 같다.

정리를 하자면

{% highlight sh %}
# .npm-global 디렉토리 생성하고 npm 구성을 변경
mkdir ~/.npm-global
npm config set prefix '~/.npm-global'   

# .profile 수정
vi ~/.profile
# .profile 맨 아래에 해당 소스 추가
export PATH=~/.npm-global/bin:$PATH
# 에디터 나가고
:wq!
# 새로 작성한 내용 적용하기
source ~/.profile
{% endhighlight %}

이걸로 .node_modules 관련 권한문제는 해결된 것 같다.   
   
## 2. Got permission denied while trying to connect to the Docker daemon socket jenkins
   
npm 권한 문제를 해결하니 도커에서도 권한 문제가 발생
도커는 접근할 때 접근할 유저의 권한을 설정해 줘야한다.
나같은 경우에는 jenkins가 접근할 권한을 줘야 됨

{% highlight sh %}
sudo /usr/sbin/groupadd -f docker
sudo /usr/sbin/usermod -a -G docker `jenkins`
sudo chown root:docker /var/run/docker.sock

# docker에 권한설정이 잘 되어있는지 확인
grep docker /etc/group

# jenkins restart
sudo service jenkins restart
{% endhighlight %}

   
젠킨스 빌드 하면서 발생하는 권한문제를 해결하는 포스팅은 여기까지
다음엔 같은 문제로 해메지 않길 ...