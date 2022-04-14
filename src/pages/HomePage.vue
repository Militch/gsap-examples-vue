<template>
    <div class="main">
        <h1>欢迎来到C位</h1>
        <p id="subtitle">即刻开启您的数字生活<br/>助力人人成为“艺术家”</p>
    </div>
</template>

<script>
import { gsap } from "gsap";
const SplitText = window.SplitText;
gsap.registerPlugin(SplitText);
export default {
  name: 'HomePage',
  data(){
    return {};
  },
  methods: {
  },
  mounted() {
    var tl = gsap.timeline(),
    mySplitText = new SplitText("#subtitle", { type: "words,chars" }),
    chars = mySplitText.chars;
    gsap.set("#subtitle", { perspective: 400 });
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
    // gsap.to('.square', {x: 500, duration: 3});
  }
}
</script>

<style>
.main {
  padding: 10em 0;
}

</style>
