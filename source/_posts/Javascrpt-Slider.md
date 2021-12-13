---
title: Javascrpt-Slider
date: 2021-12-13 20:18:36
tags: js
---

# Javascript 로 만든 슬라이더(Slider)

슬라이더(slider)는 캐로셀(Carousel)이라고도 불리는 요소로 여러 장의 이미지파일들을 나열해 회전하는 것처럼 보여준다.

먼저, Html 로 만든 구조를 javascript 에서 다룰 수 있도록 DOM 을 생성하고, 필요한 변수들을 선언한다.

```javascript
// DOM 생성
const sliderWrap = document.querySelector(".slider-wrap");
const slider = sliderWrap.querySelector(".slider");
const slideList = slider.querySelectorAll("li");
const moveBtn = sliderWrap.querySelector(".arrow");

// 슬라이드 하나의 가로길이
const liWidth = slideList[0].clientWidth;
// 슬라이드의 갯수
const slideLen = slideList.length;
// 슬라이드의 총길이
const slideWidth = liWidth * slideLen;
slider.style.width = slideWidth + "px";

// 변수
let speedTime = 500;
let moveDist = -liWidth;
let currNum = 1;

//클론생성
const firstClone = slideList[0].cloneNode(true);
const lastClone = slideList[slideLen - 1].cloneNode(true);
slider.insertBefore(lastClone, slideList[0]);
slider.appendChild(firstClone);

const slideCloneList = slider.querySelectorAll("li");
const slideCloneLen = slideCloneList.length;
console.log(slideCloneLen);
const slideCloneWidth = liWidth * slideCloneLen;
slider.style.width = slideCloneWidth + "px";
slider.style.transition = `all ${speedTime}ms ease`;

slider.style.left = `${moveDist}px`;
```
