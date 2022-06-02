---
layout: post
title: how to write markdown file
categories: study
tags: [study]
---

## 서론
나는 markdown 파일이 익숙하지가 않다.   
github.io 페이지를 블로그로 쓰려고 만들어놓고 쓸 줄을 몰라 포스팅을 한적이 없다.   
그래서 만드는 페이지! 이건 나를 위한 포스팅 :)   
가장 많이 쓰는 순서대로 작성해보자   


## 1. 줄바꿈
> 그냥 엔터만 치면 바뀔줄 알았던 줄바꿈... 띄어쓰기 3칸으로 줄을 바꿔야 한다.   
> 간단한 내용이라 예시는 생략   

## 2. code 작성
> post내에 code를 작성해야 하는 경우 사용한다.   

<pre>
  <code> 
   ```를 앞뒤로 입력하면 이와같은 코드를 작성할 수 있는 영역이 생긴다.
  </code>
</pre>
```
  `<pre><code> { code 내용 작성 } </code></pre>` 이렇게도 쓸 수 있다. 
  위쪽 소스블럭을 보면 알겠지만, 여백이 많이남아 비추. 안예쁨
```
{% highlight javascript %}
jekyll에서 지원하는 문법도 있는데... 표현할 수 있는 방법이 없다... 소스를 직접 보는 걸로
{% endhighlight %}

## 3. 이미지
> html 이미지 태그와 동일
{% highlight html %}
<img src="/assets/images/han.jpg" alt="한소희" width="100px" />
{% endhighlight %}
<img src="/assets/images/han.jpg" alt="한소희" width="100px" />

## 4. text
----------
> list type

# - order list 
{% highlight html %}
1. 1
2. 2
3. 3
{% endhighlight %}
1. 1
2. 2
3. 3   

# - unorder list 
{% highlight html %}
* *
+ +
- -
{% endhighlight %}
* *
+ +
- -

> title

```
# 1 얘만 TOC 없는 타이틀
------------
여기 아래에서부터 크기가 점점 작아지고 TOC 들여쓰기 생김
## 2 
### 3
#### 4
##### 5
```

# 1 얘만 TOC 없는 타이틀
------------
## 2 
### 3
#### 4
##### 5

> 하이퍼링크

```
[HYUZNI](https://hyuzni.github.io, "mouse over text") 
// 띄어쓰기 주의
```
[HYUZNI](https://hyuzni.github.io, "mouse over text") 

> text decoration

```
*이탤릭체*
**볼드체**
~~취소선~~
아래는 <hr>  (중간에 엔터가 한번 필요함)

--------
```
*이탤릭체*   
**볼드체**   
~~중앙선~~   
**~~볼드체중앙선~~**   
아래는 <hr>  (중간에 엔터가 한번 필요함)

--------

여기까지 끝!
추가 작성법을 알게될 때 마다 이 포스트를 수정해서 작성해보자 :)