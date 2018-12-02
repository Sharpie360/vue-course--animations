<template>
  <transition-group
    @before-enter="beforeEnter"
    @enter="enter"
    @after-enter="afterEnter"
    @enter-cancelled="enterCancelled"
    @before-leave="beforeLeave"
    @leave="leave"
    @after-leave="afterLeave"
    @leave-cancelled="leaveCancelled"
    :css="false"
  >
    <div class="box" :class="variant" v-if="loaded" key="box">
      <h3 class="box--text text-center" v-show="loaded" key="text">
        {{ text }} 
      </h3>
    </div>
  </transition-group>
</template>

<script>
export default {
  props: ['loaded', 'text', 'variant'],
  methods: {
    beforeEnter: el => {
      console.log("beforeEnter", el);
      this.boxSize = 100
      el.style.opacity = 0
      // el.style.width = this.boxSize + 'px'
    },
    enter: (el, done) => {
      console.log("enter", el, done);
      let round = 1;
      const interval = setInterval(() => {
        el.style.opacity = round / 20;
        el.style.width = (this.boxSize + round * 10) + "px";
        el.style.height = (this.boxSize + round * 10) + "px";
        round++;
        if (round > 20) {
          clearInterval(interval);
          done();
        }
      }, 20);
    },
    afterEnter: el => {
      const text = el.children[0]
      console.log(text)
      text.style.opacity = 1;
    },
    enterCancelled: el => {
      // console.log("enterCancelled");
    },
    beforeLeave: el => {
      console.log("beforeLeave");
      this.boxSize = 300
      el.style.width = this.boxSize + 'px'
    },
    leave: (el, done) => {
      const text = el.children[0]
      console.log('leave', text)
      text.style.opacity = 0
      // console.log("leave", el, done);
      const roundMax = 20;
      let round = 1;
      const interval = setInterval(() => {
        el.style.opacity = 1 / 20 * (roundMax - round);
        el.style.width = (this.boxSize - round * 10) + 'px'
        el.style.height = (this.boxSize - round * 10) + 'px'
        round++;
        if ((round > roundMax)) {
          clearInterval(interval);
          done();
        }
      }, 20);
    },
    afterLeave: el => {
      console.log('afterleave:', el);
    },
    leaveCancelled: el => {
      // console.log("leaveCancelled");
    }
  }
}
</script>

<style>
/* custom box div */
.box {
  width: 8rem; 
  height: 8rem; 
  background-color: transparent;
  border: 3px solid #f7f7f7;
  border-radius: 7px;
	padding: 1rem;
	box-shadow: 2px 2px 10px rgba(127, 127, 127, 0.3);
	display: flex;
	flex: 1;
	justify-content: center;
	align-items: center;
}

.box--text {
	opacity: 0;
}

.box--box1 {
  background-color: #00d6a4;
}
.box--box2 {
  background: linear-gradient(90deg, #00d6a4, #006473);
}
.box--box3 {
  background-color: #006473;
}

</style>
