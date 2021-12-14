---
title: Javascript 로 만든 슬라이더(Slider)-2
date: 2021-12-13 20:18:36
tags: js
---

슬라이더(slider)는 캐로셀(Carousel)이라고도 불리는 요소로 여러 장의 이미지파일들을 나열해 회전하는 것처럼 보여준다.

Html 로 만든 구조위에 css 로 슬라이더의 기본 모양을 만등 후 javascript 에서 다룰 수 있도록 DOM 을 생성하고, 필요한 변수들을 선언한다.

내부에 2개의 a tag("이전, "다음")가 있는 버튼을 한개만 만들어  
이벤트를 붙이면 버블링효과로 인해 코드가 훨씬 간결해 진다.
또, 사진을 옯기는 방식도 slider {transform : translateX(800px)} 과 같은 방식보다 position 층으로 띄운 slider 의 left 값을 옮길 가로넓이 만큼 계산해서 주면 간결해진다. <정을수 강사님 강의를 참조함>

```javascript
// DOM 생성
const sliderWrap = document.querySelector(".slider_wrap");
const sliderBox = sliderWrap.querySelector(".slider_box");
const slider = sliderBox.querySelector(".slider");
const sliders = slider.querySelectorAll("li");
const moveButton = sliderWrap.querySelector(".arrow");

// 슬라이더 총길이 계산
const liwidth = sliders[0].clientWidth;
const liLength = sliders.length;
const sliderLen = liwidth * liLength;
slider.style.width = liwidth * liLength + "px";

let moveDist = 0;
// 화면이 자연스럽게 넘어가도록 transition 값을 준다.
let speedTime = 500;

moveButton.addEventListener("click", moveSlide);

function moveSlide(e) {
  e.preventDefault();
  if (e.target.className === "next") {
    // next 버튼을 누르면 현재 보고 있는 이미지는 왼쪽으로 이동하므로
    // 즉, css로 position 층으로 띄운 slider 의 left 값을 음수를 줘서
    // 현재 보고 있는 이미지를 왼쪽으로 이동시킨다.
    moveDist -= liwidth;
    slider.style.left = `${moveDist}px`;
    slider.style.transition = `all ${speedTime}ms ease`;
  } else {
    // prev 버튼은 next의 반대로
    moveDist += liwidth;
    slider.style.left = `${moveDist}px`;
    slider.style.transition = `all ${speedTime}ms ease`;
  }
}
```

그러나, 맨앞과 맨뒤 이미지에서 멈추게 되면, 슬라이더라고 할 수 없으니 다음화에서 고쳐보겠다.
