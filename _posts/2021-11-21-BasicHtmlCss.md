---
title: "Html+CSS Basic"
categories:
    - FrontEnd Web Development
tags:
    - [html]
date: 2021-09-26 
use_math : true
---
- Header tag는 HTML heading tags 의 part of the subset (h1~h6)
- Classes는 css를 통하여 style 혹은 format을 바꿀 수 있는 한가지 방법

~~~css
header .profile-image:hover {
	  transform: scale(3) rotate(720deg);
}
~~~
위의 예시는 hover : 마우스를 올렸을 때 , transform 3배 커지고 2바퀴 돌리라는 것   

webdevelopment 는 **Front End Development**(Html, CSs), **Back End Development**(python , retrieving data from database server) 로 나누어짐 

---
- Html
  - Head : contains a lot of behind the scenes information that people won't see 
    - title 
    - css와 엮어주는 링크
    - javascript 와 엮어주는 코드
    - meta tag 
  - Body :  contains everything you see in the browser (아래는 예시) 
    - header : company logo, name of the site, purpose of the site 와 같은 introductory information 을 담고 있음  
    - main : contain bulk of the content to share with worlds!(블로그 같으면 포스트)
    - footer : copyright information 이나 secondary navigation 등 부가적인 기능 

- doc type(Html 밖에 있는 코드 ) : always first 

---
### **Html 태그 종류**      
- image : image attribute 는 source attribute 와 alt attribute(파일 깨졌을 때 나오는 설명) 를 반드시 포함해야 함 또한 closing tag 가 필요없음
    ```html
    <img src="images/me.png" alt="Drawing of Jane Smith" class="profile-image">
    ```
    위의 코드는 src , alt, class 3개의 attribute 를 가지고 있음  
    
- paragraph: 가독성을 위해 두 문단 사이에 space 를 주기도 함(margin) ```<p></p>``` 태그
  
- Link:

    ```html 
    <p><a>next paragraph</a></p>
    ```

    <p><a>next paragraph</a></p> 위처럼 링크화 된다

    ```html 
    <p><a href="#">next paragraph</a></p>
    ``` 

    <p><a href="#">next paragraph</a></p> -> 누르면 위로 올라감 (#=#top)
    
    ```html
     <p><a href="www.google.co.kr" target="_blank ">next paragraph</a></p>
    ``` 
    이걸 하면 현재 창 말고 다른 창에서 해당 링크를 띄워준다. 다른 탭에서 열기 ? 
- list
  - ul : unordered list
  - ol : ordered list 
    ```html
    <ol>
        <li>hi
        </li>
        <li>I am
        </li>
    </ol>
    ```
    은 숫자 , ul 로 바꾸어 주면 $\cdot$ 이런 글머리 기호로 나옴 
    <ol>
        <li> hi
        </li>
        <li>I am
        </li>
    </ol>

---
### **CSS**
```css
body {
  margin: 0;
  padding: 0;
  text-align: center;
  font-family: 'Roboto', sans-serif;
  color: #222;
  background: #f7f5f0;
}
```

이런 것들을 css rule 이라고 부름
```css
a {
  text-decoration: none;
  color: #0499ff;
}
```
이 rule 은 anchor 들을 이 color로 해라는 것 각각의 rule 들은 selector(여기서는 a, 어떤 html tag 나 class, element 를 style 할건지)  
#### CSS Property
- color -> ```color```
- letter spacing -> ```letter-spacing```
- font size -> ```
- line height
- margin
- border -> ``` border: solid black 3pxs ```
- border-round -> square image 에 50퍼 적용하면 원이 됩니다 
- padding and margin -> padding 은 border 안을 늘리고 , margin 은 border 바깥을 늘림 

> 그러면 어떻게 하면 같은 태그를 가진 것중, 하나만 style을 바꿀 수 있을까 ?  

일단 
```html
<main class="flex">
    <div class="card">
        <h2 class="card-title">Background</h2>
```
대충 card 밑에 있으니 card-title 이라는 클래스 이름을 짓고 , css 에 가서 

```css
.card-title{
    text-align : center;
}
``` 
이런식으로 하면 h2 태그 전체를 바꾸지 않고도, card-title 이름을 가진 class 의 style 만 바꿀 수 있다. (css style 사이트 css-tricks.com 추천)  

