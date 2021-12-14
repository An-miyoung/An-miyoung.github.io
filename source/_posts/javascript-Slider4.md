---
title: Javascript 로 만든 슬라이더(Slider)-4
date: 2021-12-14 22:33:27
tags: vanillaJS
---

각 이미지들이 자연스럽게 넘어가도록 준,  
 transition 효과가 마지막 이미지에서 다음 이미지로 연결될때  
 자연스럽지 않아서 슬라이더가 맨앞 혹은 마지막에 왔을때  
 setTimeout 함수를 사용해 잠시 transition을 멈춘 후
다시 transition 이 일어나게 한다.<정을수 강사님 강의를 참조함>

```javascript
function moveSlide(e) {
  e.preventDefault();
  if (e.target.className === "next") {
    move(-1);
    if (currNum === cloneLength - 1) {
      setTimeout(() => {
        slider.style.transition = "none";
        moveDist = -liwidth;
        currNum = 1;
        slider.style.left = `${-liwidth}px`;
      }, speedTime);
    }
  } else {
    move(1);
    if (currNum === 0) {
      setTimeout(() => {
        slider.style.transition = "none";
        currNum = cloneLength - 2;
        moveDist = -(liwidth * currNum);
        slider.style.left = `${moveDist}px`;
      }, speedTime);
    }
  }
  function move(direction) {
    currNum += -1 * direction;
    moveDist += liwidth * direction;
    slider.style.transition = `all ${speedTime}ms ease`;
    slider.style.left = `${moveDist}px`;
  }
}
```
