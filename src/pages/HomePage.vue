<template>
    <div class="main">
        <h1>欢迎来到C位</h1>
        <p id="subtitle">即刻开启您的数字生活<br/>助力人人成为“艺术家”</p>
	<hr/>
	<div class="container">
            <div class="card card-one" @click="handleCardOneClick">
                卡片1
            </div>
            <div class="card card-two" @click="handleCardTwoClick">
                卡片2
            </div>
            <div class="card card-three" @click="handleCardThreeClick">
                卡片3
            </div>
        </div>
    </div>
</template>

<script>
import { gsap } from "gsap";
const SplitText = window.SplitText;
gsap.registerPlugin(SplitText);
export default {
  name: 'HomePage',
  data(){
    return {
        top: 1,
    };
  },
  methods: {
    topOneCard(dep){
	let tl = dep?dep:gsap.timeline();
	tl.to('.card-one', {x: -100, duration: 0.5});
	tl.set('.card-one', {css: {zIndex: 999}});
	tl.set('.card-two', {css: {zIndex: 998}});
	tl.set('.card-three', {css: {zIndex: 997}});
	tl.to('.card-one', {x: 0, duration: 0.5});
    },
    topTwoCard(left){
	let tl = gsap.timeline();
	tl.to('.card-two', {x: left?-100:100, duration: 0.5});
	tl.set('.card-one', {css: {zIndex: 998}});
	tl.set('.card-two', {css: {zIndex: 999}});
	tl.set('.card-three', {css: {zIndex: 998}});
	tl.to('.card-two', {x: 0, duration: 0.5});
	return tl;
    },
    topThreeCard(dep){
	let tl = dep?dep:gsap.timeline();
	tl.to('.card-three', {x: 100, duration: 0.5});
	tl.set('.card-one', {css: {zIndex: 998}});
	tl.set('.card-two', {css: {zIndex: 998}});
	tl.set('.card-three', {css: {zIndex: 999}});
	tl.to('.card-three', {x: 0, duration: 0.5});
    },
    handleCardOneClick(){
	if (this.top === 2){
            this.topOneCard();
            this.top = 1;
	}else if (this.top === 3){
            let depTl = this.topTwoCard(true);
            this.topOneCard(depTl);
            this.top = 1;
	}
    },

    handleCardTwoClick(){
	if (this.top === 1){
            this.topTwoCard();
            this.top = 2;
	}else if(this.top === 3){
            this.topTwoCard(true);
            this.top = 2;
	}
    },
    handleCardThreeClick(){
	if (this.top === 1){
            let depTl = this.topTwoCard();
            this.topThreeCard(depTl);
            this.top = 3;
	}else if (this.top === 2){
            this.topThreeCard();
            this.top = 3
	}
    },
  },
  mounted() {
    var tl = gsap.timeline(),
    // 拆分文字
    mySplitText = new SplitText("#subtitle", { type: "words,chars" }),
    chars = mySplitText.chars;
    gsap.set("#subtitle", { perspective: 400 });
    // 副标题入场动画
    tl.from(chars, {
      duration: 0.8,
      opacity: 0,
      scale: 0,
      y: 80,
      rotationX: 180,
      transformOrigin: "0% 50% -50",
      ease: "back",
      stagger: 0.01
    });
    // 卡片入场动画
    var t2 = gsap.timeline();
    t2.from('.card-one', {x: 320, duration: 0.5});
    t2.from('.card-two', {x: 150, duration: 0.5});
    t2.from('.card-three', {x: 100, duration: 0.5});
  }
}
</script>

<style>
.main {
  padding: 10em 0;
}
.container {
  display: flex;  
  justify-content: center;
}

.card {
  width: 10em;
  height: 10em;
  line-height: 10em;
  color: #ffffff;
  background-color: #ff0000;
  cursor: pointer;
}
.card-one {
  background-color: #f5222d;
  margin: 0 -3em;
  z-index: 999;
}
.card-two {
  background-color: #52c41a;
  margin: 0 -3em;
  z-index: 998;
}
.card-three {
  background-color: #1890ff;
  margin: 0 -3em;
  z-index: 997;
}
h1 {
 font-size: 4em;
}
#subtitle {
  font-size: 2em;
}
</style>
