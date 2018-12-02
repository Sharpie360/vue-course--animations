<template>
  <div class="container">
    <div class="row">
      <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3 mt-5">
        <h1>Vue.js Animations</h1>
        <h3>
          <span @click="cssAnimations = true" class="pointer">CSS</span>
          or
          <span @click="cssAnimations = false" class="pointer">JS</span>?
        </h3>
        <hr>
        <div v-if="cssAnimations">
          <select class="form-control" v-model="selectedAnimation">
            <option value="slide-left">Slide Left</option>
            <option value="slide-right">Slide Right</option>
          </select>
          <hr>
          <button class="btn btn-primary mb-3" @click="show = !show">Show Alert Animations</button>
          <transition enter-active-class="animated pulse" leave-active-class="animated pulse">
            <div class="alert alert-warning" v-if="show">AnimateCSS Animations</div>
          </transition>
          <transition name="fade" type="transition">
            <div
              class="alert alert-primary"
              v-if="show"
            >an alert box using the transition class anim hooks</div>
          </transition>
          <transition name="slide-left" type="animation">
            <div class="alert alert-info" v-if="show">
              <h2 class="mb-1">This is an alert box!</h2>
            </div>
          </transition>
        </div>
        <div v-else>
          <h4 class="mb-3">Javascript Animations</h4>

          <button class="btn btn-success" @click="loaded = !loaded">Load / Remove Element</button>
          <hr>

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
            <div class="box" v-if="loaded" key="box">
							<h3 class="box--text text-center" v-show="loaded" key="text">
								Hello from inside the box! 
							</h3>
						</div>
          </transition-group>
        </div>
      </div>

      <div 
				class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3 mt-5 pt-4" 
				v-if="cssAnimations">
        <!-- 
                    transition between different elements 
                    always check the type against the action
                    set the mode for when to trigger next element animation
        -->
					<transition :name="selectedAnimation" type="animation" mode="out-in">
						<div class="alert alert-info" v-if="show" key="off">OFF</div>
						<div class="alert alert-primary" v-else key="on">ON</div>
					</transition>
					<transition name="fade" type="transition" mode="out-in">
						<div class="alert alert-info" v-if="show" key="off2">OFF</div>
						<div class="alert alert-primary" v-else key="on2">ON</div>
					</transition>

					<div class="card">
						<h5 class="card-header">Animation with Vue</h5>
						<div class="card-body expand-body" v-if="show">
							<ul class="list-group list-group-flush">
								<transition-group name="slide-right">
									<li
										class="list-group-item"
										v-for="(item, i) in 5"
										:key="i"
									>Some fancy list items here</li>
								</transition-group>
							</ul>
						</div>
					</div>
      </div>

			<div 
				class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3 mt-5 pt-4"
				v-else>

			</div>
    </div>
  </div>
</template>

<script>
import Navbar from './components/Navbar'
import SuccessAlert from './components/SuccessAlert'
import DangerAlert from './components/DangerAlert'

export default {
  data() {
    return {
      cssAnimations: true,
      show: false,
      loaded: false,
      selectedAnimation: "",
			boxSize: 100,
			showBoxMessage: false
    };
	},
	components: {
		'success-alert': SuccessAlert,
		'danger-alert': DangerAlert
	},
  methods: {

		toggleMsg() {
			this.showBoxMessage = !this.showBoxMessage
			console.log('test')
		},
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
};
</script>

<style>
body {
  background-color: #212121;
  color: #f7f7f7;
}

.pointer {
  cursor: pointer;
}

.alert {
  color: #f7f7f7;
}
.alert-primary {
  background-color: #03a9ac;
}
.alert-success {
  background-color: #00d6a4;
}
.alert-info {
  background-color: rgba(3, 216, 203, 0.2);
}
.alert-warning {
  background-color: rgb(245, 125, 125);
}

.card-header {
  color: #03a9ac;
}
.card-body {
  color: #4b4b4b;
}

/* custom box div */
.box {
  width: 8rem; 
  height: 8rem; 
  background-color: #00d6a4;
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


/*
==============================================
= VUE.JS CSS ANIMATION CLASSES AND KEYFRAMES =
==============================================
*/

.fade-enter {
  opacity: 0;
  transform: translateY(-1rem);
}
.fade-enter-active {
  transition: all 0.3s ease-in-out;
}

.fade-leave-active {
  transition: all 0.3s ease-in-out;
}
.fade-leave-to {
  opacity: 0;
  transform: translateY(1rem);
}

.slide-left-enter {
  opacity: 0;
}
.slide-left-enter-active {
  animation: slide-in-left 0.5s ease-in-out forwards;
  transition: opacity 0.3s;
}

.slide-left-leave-active {
  animation: slide-out-left 0.3s ease-in-out forwards;
  transition: opacity 0.5s;
}
.slide-left-leave-to {
  opacity: 0;
}

.slide-right-enter {
  opacity: 0;
}
.slide-right-enter-active {
  animation: slide-in-right 0.5s ease-in-out forwards;
  transition: opacity 0.3s;
}

.slide-right-leave-active {
  animation: slide-out-right 0.3s ease-in-out forwards;
  transition: opacity 0.5s;
}
.slide-right-leave-to {
  opacity: 0;
}

@keyframes slide-in-left {
  from {
    transform: translateX(-2rem);
  }
  50% {
    transform: translateX(0.5rem);
  }
  to {
    transform: translateX(0);
  }
}

@keyframes slide-out-left {
  from {
    transform: translateX(0rem);
  }
  50% {
    transform: translateX(0.5rem);
  }
  to {
    transform: translateX(-2rem);
  }
}

@keyframes slide-in-right {
  from {
    transform: translateX(2rem);
  }
  50% {
    transform: translateX(-0.5rem);
  }
  to {
    transform: translateX(0);
  }
}

@keyframes slide-out-right {
  from {
    transform: translateX(0rem);
  }
  50% {
    transform: translateX(-0.5rem);
  }
  to {
    transform: translateX(2rem);
  }
}
</style>
