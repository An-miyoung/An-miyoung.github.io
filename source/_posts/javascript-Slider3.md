---
title: Javascript 로 만든 슬라이더(Slider)-3
date: 2021-12-14 21:15:05
tags: vaniilaJS
---

지난 회에 3장의 이미지가 앞,뒤로 움직이게 만들었지만,  
첫번째 이미지 "이전"과 마지막 이미지 "이후"는 작동하지 않았다.  
원래 슬라이더는 맨 앞 이미지와 맨 뒤 이미지가 연결된 것 처럼 움직이므로 연결시켜 보겠다.
방식은 첫번째 이미지 앞에 마지막 이미지를 붙이고,  
마지막 이미지 뒤에 맨앞 이미지를 붙여서 해결해 보겠다.<정을수 강사님 강의를 참조함>

```javascript
const sliderWrap = document.querySelector(".slider_wrap");
const sliderBox = sliderWrap.querySelector(".slider_box");
const slider = sliderBox.querySelector(".slider");
const sliders = slider.querySelectorAll("li");
const moveButton = sliderWrap.querySelector(".arrow");
const liwidth = sliders[0].clientWidth;
const liLength = sliders.length;

// cloneNode를 만들어 맨앞과 맨뒤에 붙이기
const firstChild = sliders[0].cloneNode(true);
const lastChild = sliders[liLength - 1].cloneNode(true);
slider.insertBefore(lastChild, sliders[0]);
slider.appendChild(firstChild);

// 슬라이더 총길이 계산
const sliderClone = slider.querySelectorAll("li");
const cloneLength = sliderClone.length;
const sliderLen = liwidth * cloneLength;
slider.style.width = sliderLen + "px";

//
let moveDist = -liwidth;
let speedTime = 500;
let currNum = 1;
slider.style.left = `${moveDist}px`;

moveButton.addEventListener("click", moveSlide);

function moveSlide(e) {
  e.preventDefault();
  if (e.target.className === "next") {
    if (currNum === cloneLength - 1) {
      moveDist = 0;
      currNum = 0;
      slider.style.left = `${moveDist}px`;
      slider.style.transition = `all ${speedTime}ms ease`;
    } else {
      moveDist += -liwidth;
      currNum += 1;
      slider.style.left = `${moveDist}px`;
      slider.style.transition = `all ${speedTime}ms ease`;
    }
  } else {
    if (currNum === 0) {
      currNum = cloneLength - 1;
      moveDist = -(liwidth * currNum);
      slider.style.left = `${moveDist}px`;
      slider.style.transition = `all ${speedTime}ms ease`;
    } else {
      moveDist += liwidth;
      currNum -= 1;
      slider.style.left = `${moveDist}px`;
      slider.style.transition = `all ${speedTime}ms ease`;
    }
  }
}
```

코드내에서 많은 반복구문이 있어서 반복되는 부분을 함수로 만들어보면,

```javascript
function moveSlide(e) {
  e.preventDefault();
  if (e.target.className === "next") {
    move(-1);
    if (currNum === cloneLength - 1) {
      moveDist = 0;
      currNum = 0;
      slider.style.left = `${moveDist}px`;
      slider.style.transition = `all ${speedTime}ms ease`;
    }
  } else {
    move(1);
    if (currNum === 0) {
      currNum = cloneLength - 1;
      moveDist = -(liwidth * currNum);
      slider.style.left = `${moveDist}px`;
      slider.style.transition = `all ${speedTime}ms ease`;
    }
  }
  function move(direction) {
    currentNum += -1 * direction;
    moveDist += liWidth * direction;
    slider.style.transition = `all ${speedTime}ms ease`;
    slider.style.left = `${moveDist}px`;
  }
}
```
