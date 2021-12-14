---
title: Javascript 로 만든 슬라이더(Slider)-1
date: 2021-12-14 19:55:35
tags: js
---

슬라이더(slider)는 캐로셀(Carousel)이라고도 불리는 요소로 여러 장의 이미지파일들을 나열해 회전하는 것처럼 보여준다.

먼저, Html 로 만든 구조를 만든다. <정을수 강사님 강의를 참조함>

```html
<body>
  <div class="slider_wrap">
    <div class="slider_box">
      <ul class="slider">
        <li>
          <img src="https://via.placeholder.com/800x200.png?text=1" alt="" />
        </li>
        <li>
          <img src="https://via.placeholder.com/800x200.png?text=2" alt="" />
        </li>
        <li>
          <img src="https://via.placeholder.com/800x200.png?text=3" alt="" />
        </li>
      </ul>
    </div>
    <div class="arrow">
      <a href="" class="prev">이전</a>
      <a href="" class="next">다음</a>
    </div>
  </div>
</body>
```

css로 슬라이더의 모양을 만든다.

```css
* {
  margin: 0;
  padding: 0;
}
a {
  text-decoration: none;
}
li {
  list-style: none;
}
.slider_wrap {
  width: 100%;
  max-width: 800px;
  margin: 0 auto;
  position: relative;
}
.slider_wrap > .slider_box {
  overflow: hidden;
  position: relative;
  height: 200px;
}
.slider_wrap > .slider_box .slider {
  position: absolute;
  top: 0;
  left: 0;
}
.slider_wrap > .slider_box .slider > li {
  float: left;
}
.slider_wrap > .slider_box .slider > li img {
  vertical-align: top;
}
.slider_wrap .arrow > a.prev {
  position: absolute;
  left: -50px;
  top: 100px;
}
.slider_wrap .arrow > a.next {
  position: absolute;
  right: -50px;
  top: 100px;
}
```
