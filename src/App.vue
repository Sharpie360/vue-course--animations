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
            <option selected value="slide-left">Slide Left</option>
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

				

      </div>

			<!-- click toggle alerts -->
      <div 
				class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3 mt-5 pt-4" 
				v-if="cssAnimations">
        <!-- 
                    transition between different elements 
                    always check the type against the action
                    set the mode for when to trigger next element animation
        -->
				<div @click="clickAlert_1 = !clickAlert_1">
					<transition :name="selectedAnimation" type="animation" mode="out-in">
						<div class="alert alert-info" v-if="clickAlert_1" key="off">OFF</div>
						<div class="alert alert-primary" v-else key="on">ON</div>
					</transition>
				</div>
				<div @click="clickAlert_2 = !clickAlert_2">
					<transition name="fade" type="transition" mode="out-in">
						<div class="alert alert-info" v-if="clickAlert_2" key="off2">Click to turn me OFF!</div>
						<div class="alert alert-primary" v-else key="on2">Click to turn me ON!</div>
					</transition>
				</div>

					<list></list>

      </div>

			<!-- dynamic component transitions -->
			<div 
				class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3 mt-5 pt-4"
				v-else>
				<button 
					@click="selectedCmp === 'success-alert' ? selectedCmp = 'danger-alert' : selectedCmp = 'success-alert'"
					class="btn btn-danger mb-3"
					>Toggle Alerts
				</button>
				<transition name="fade" mode="out-in">
					<component :is="selectedCmp"></component>				
				</transition>
			</div>

			<!-- javascript hook animations/transitions -->
			<boxes></boxes>

    </div>
  </div>
</template>

<script>
import Navbar from './components/Navbar.vue'
import SuccessAlert from './components/SuccessAlert.vue'
import DangerAlert from './components/DangerAlert.vue'
import Boxes from './components/Boxes.vue'
import List from './components/List.vue'

export default {
  data() {
    return {
      cssAnimations: true,
			show: false,
			clickAlert_1: true,
			clickAlert_2: true,
      selectedAnimation: "",
			boxSize: 100,
			showBoxMessage: false,
			selectedCmp: 'success-alert'
    };
	},
	components: {
		'success-alert': SuccessAlert,
		'danger-alert': DangerAlert,
		'boxes': Boxes,
		'list': List
	},
  methods: {

		toggleMsg() {
			this.showBoxMessage = !this.showBoxMessage
			console.log('test')
		},
  
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
.flexbox-space-evenly {
	display: flex;
	flex: 1;
	justify-content: space-evenly;
}
.flex-vert {
	align-items: center;
}


.alert {
  color: #f7f7f7;
}
.alert-primary {
  background-color: rgb(3, 169, 172);
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
.alert-danger {
	background-color: #fa423e;
}

.card-header {
  color: #03a9ac;
}
.card-body {
  color: #4b4b4b;
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
