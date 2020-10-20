<template>
<!-- <div>
  <div class="blank"/>
  <div class="wrapper">
  <div class="first">
    <canvas class="img1" />
    <h2 class="title1">Hello World!</h2>
</div>
    <div class="img2" />
    <h2 class="title2 white-text">Hello Mike</h2>
    </div>
  <div class="blank"/>
</div> -->
<div id="app">
  <div class="pinContainer" ref="pin">
    <section v-for="(p, index) in panels" class="panel" :class="`panel-${index}`" :key="index" :style="{backgroundColor: p.bgColor}" >
      <h1>{{ p.title }}</h1>
      <p>{{p.quote}}</p>
    </section>
  </div>
</div>
<!-- <div>
<header class="header section">
  <div class="center">&darr;</div>
</header>

<section class="scene section" ref="sticky" id="sticky">
  <div class="viewer"></div>
</section>

<section class="section">
  <div class="center">End</div>
</section>
</div> -->
</template>

<script>
import 'gsap'
// import 'ScrollToPlugin'
export default {
  components: {},
    data() {
    return {
      panels: [
        {
          title: "panel 1",
          bgColor: "#29b6f6",
          quote:
            "Mountains are the beginning and the end of all natural scenery."
        },
        {
          title: "panel 2",
          bgColor: "#ef5350"
        },
        {
          title: "panel 3",
          bgColor: "#ec407a"
        },
        {
          title: "panel 4",
          bgColor: "#66bb6a"
        },
          {
          title: "panel 5",
          bgColor: "#150259"
        },
          {
          title: "panel 6",
          bgColor: "#000000"
        }
      ]
    };
  },
mounted () {
    // this.startAnimation()
     this.$nextTick(this.pinContainerScene);
  },
  methods: {
  //   startAnimation(){
  //     // const controller = new this.$scrollmagic.controller()
  //     var tl = new TimelineMax({onUpdate: updatePercentage})

  //     tl.to('.first', 1, {width: '100%'}, 0)
  //     tl.to('.title1', 0.5, {opacity: 1}, 1)
  //     tl.to('.title2', 0.5, {opacity: 0}, 2)
  //     tl.to('.img2', 1, {height: '100%'}, 2)
  //     tl.from('.title2', 1, {opacity: 0}, 2.1)
  //     tl.to('.img1', 0, {opacity: 0}, 3)
  //     tl.to('.title1', 0, {opacity: 0}, 3)
  //     tl.to('.img2', 1, {width: '50%', height: '50%', transform: 'translate(-25%, -30%)'}, 3)
  //     tl.to('.title2', 1, {color: 'rgba(255, 255, 255, 0)'}, 3)

  //     const scene = this.$scrollmagic.scene({
  //       triggerElement: '.wrapper',
  //       triggerHook: 0,
  //       duration: '300%'
  //     })
  //     .setPin(".wrapper")
  //     .setTween(tl)

  //     this.$scrollmagic.addScene(scene)

  //     function updatePercentage(){
  //       tl.progress()
  //     }
  // }
  pinContainerScene() {
      const Length = this.panels.length;
      console.log(Length)

      // Create a new Timeline (equivalent to new TimelineMax())
      const tl = new this.$gsap.TimelineMax();

      for (var i = 0; i < Length; i++) {
        // For each panel in this.panels array:
        let animFrom, animOutLetters;
        switch (i) { // Set animFrom value, depending on the index i of the item
          case 0:
            break; // First panel is already visible on page load, so no animation
          case 1:
            animFrom = { x: "-100%" }; // Second panel comes from the left
            break;
          case 2:
            animFrom = { x: "100%" }; // Third one comes from the right
            break;
          case 3:
            animFrom = { y: "-100%" }; // Finally, the last one comes from the top
            break;
               case 4:
            animFrom = { y: "100%" }; // Third one comes from the right
            break;
          case 5:
            animFrom = { x: "-100%" }; // Finally, the last one comes from the top
            break;
        }
        if (i !== 0) {
          // For each panel except the one whom index is 0, create the tween and add it to the tl timeline
          tl.fromTo(`section.panel-${i}`, 1.5, animFrom, {
            x: "0%",
            y: "0%",
            ease: Linear.easeNone
          });
        }
      }

      // create scene and set its params
      const scene = new this.$scrollmagic.Scene({
        triggerElement: ".pinContainer",
        triggerHook: "onLeave",
        duration: `${Length * 200}%` // each panel animation will last 200% of the screen's height
      })
        .setPin(".pinContainer")
        .setTween(tl);

      // Add scene to ScrollMagic controller by emiting an 'addScene' event on vm.$ksvuescr (which is our global event bus)
      this.$ksvuescr.$emit("addScene", "pinContainerScene", scene);

      // TAAAAAAADAAAAAAAAAAAA
    }
}
}
</script>

<style lang="scss" scoped>
// html{
//   box-sizing: border-box;
//   font-size: 100%;
// }

// *, *:before, *:after {
//   box-sizing: inherit;
//   margin: 0;
//   padding: 0;
// }

// body{
//   width: 100%;
//   -webkit-font-smoothing: antialiased;
//   font-family: 'Open Sans', sans-serif;
//   overflow-x: hidden;
//   // color: #000;
//   font-size: 16px;
// }

// .blank{
//   width: 100%;
//   height: 100vh;
// }

// .wrapper{
//   width: 100%;
//   height: 100vh;
//   position: relative;
//   overflow: hidden;
// }
// .first{
//   width: 80vw;
//   height: 100vh;
//   margin-left: auto;
//   margin-right: auto;
// }

// .img1{
//   background-image:url('../assets/img/bg1.jpg') ;
//   width: 100%;
//   height: 100%;
//   background-size: cover;
//   background-repeat: no-repeat;
//   background-position: center;
// }

// .title1{
//   position: absolute;
//   top: 50%;
//   left: 20%;
//   font-size: 32px;
//   transform: translate(-50%, -50%);
//   opacity: 0;
// }

// .img2{
//   background-image:url('../assets/img/bg.jpg') ;
//   width: 100%;
//   height: 0;
//   position: absolute;
//   bottom: 0;
//   left: 49.9%;
//   transform: translate(-50%, 0);
//   background-size: 100%;
//   background-repeat: no-repeat;
//   background-position: center bottom;
// }
// // .img3{
// //   background-image:url('../assets/img/bg2.jpg') ;
// //   width: 100%;
// //   height: 0;
// //   position: absolute;
// //   bottom: 0;
// //   left: 50%;
// //   transform: translate(-50%, 0);
// //   background-size: 100%;
// //   background-repeat: no-repeat;
// //   background-position: center bottom;
// // }

// .title2{
//   position: absolute;
//   top: 50%;
//   left: 50%;
//   font-size: 60px;
//   transform: translate(-50%, -50%);
//   transform-origin: center;
//   text-align: center;
//   line-height: 60px;
// }

// DEMO GLOBALS
// ==========================================================

// html,
// body {
//   height:100vh;
//   margin: 0;
// }

// body {
//   width:100%;
// }

// // UTILITIES
// // ==========================================================

// .header {
//   color: white;
//   font-size: 50px;
// }

// .section {
//   height: 50vh;
//   background: #293744;
//   color: #899eb5;
// }

// .scene {
//   height: 100%;
//   width: 100%;
//   background: #EAEAEA;
// }

// .center {
//   display: flex;
//   justify-content: center;
//   align-items: center;
//   height: 100%;
// }

// // REQUIRED STYLES
// // ==========================================================

// $frame-count: 9;
// $offset-val: 100;

// .viewer {
//   // CSS ONLY EXAMPLE
//   // animation: drink-coffee 1s steps($frame-count) infinite;
//   height: 100vh;
//   margin-left: auto;
//   margin-right: auto;
//   max-width: 200px;
//   width: 100%;
//   background-image: url(https://s3-us-west-2.amazonaws.com/s.cdpn.io/210284/doodle-sprite.png);
//   background-repeat: no-repeat;
//   background-position: 0 50%;
// }

// @for $i from 1 through $frame-count {
//   .viewer.frame#{$i} {
//     background-position: -(($i * $offset-val) * 2) + px 50%;
//   }
// }

// // CSS ONLY EXAMPLE
// @keyframes drink-coffee {
//   to {
//     background-position: -1800px 50%;
//   }
// }

  body {
    margin: 0;
  }
  .pinContainer {
    width: 100%;
    height: 100vh;
    overflow: hidden;
    position: relative;
  }
  .panel {
    height: 100%;
    width: 100%;
    position: absolute;
    top: 0;
    left:0;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    color: white;
    font-size: 3rem;
  }

</style>
