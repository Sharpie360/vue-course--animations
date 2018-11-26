<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3 mt-5">
                <h1>Vue.js Animations</h1>
                <hr>
                <select class="form-control" v-model="selectedAnimation">
                    <option value="fade">Downwards Fade</option>
                    <option value="slide-left">Slide Left</option>
                    <option value="slide-right">Slide Right</option>
                </select>
                <hr>
                <button class="btn btn-primary mb-3" @click="show = !show">Show Alert Animations</button>
                <transition name="fade" type="transition">
                    <div class="alert alert-primary" v-if="show">This is an alert box!</div> 
                </transition>
                <transition name="slide-left" type="animation">
                    <div class="alert alert-info" v-if="show">
                        <h2 class="mb-1">This is an alert box!</h2>
                    </div> 
                </transition>
                <transition name="slide-right" type="animation" appear>
                    <div class="alert alert-info" v-if="show">OFF</div> 
                    <div class="alert alert-primary" v-else>This is an alert box DANGER op.</div> 
                </transition>
                <transition
                    enter-active-class="animated pulse"
                    leave-active-class="animated pulse">
                    <div class="alert alert-warning" v-if="show">Some Cool Animations</div>
                </transition>
                
            </div>
            <!-- <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3 mt-5 pt-4">
                <div class="card">
                    <h5 class="card-header">Animation with Vue</h5>
                    <div class="card-body expand-body" v-if="show">
                        <ul class="list-group list-group-flush">
                            <transition-group name="slide-right">
                                <li class="list-group-item" v-for="(item, i) in 5" :key="i">
                                    Some fancy list items here
                                </li>
                            </transition-group>
                        </ul>
                    </div>
                </div>
            </div> -->
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                show: false,
                showSecond: false,
                selectedAnimation: 'fade'
            }
        }
    }
</script>

<style>
body {
    background-color: #212121;
    color: #f7f7f7
}

.alert {
    color: #f7f7f7;
}
.alert-primary {
    background-color: #03A9AC;
}
.alert-success {
    background-color: #00d6a4;
}
.alert-info {
    background-color: rgba(3, 216, 203, .2);
}

.card-header {
    color: #03A9AC
}
.card-body {
    color: #4b4b4b
}


.fade-enter {
    opacity: 0;
    transform: translateY(-1rem);
}
.fade-enter-active {
    transition: all .3s ease-in-out;
}

.fade-leave-active {
    transition: all .3s ease-in-out;
}
.fade-leave-to {
    opacity: 0;
    transform: translateY(1rem)
}

.slide-left-enter {
    opacity: 0;
}
.slide-left-enter-active {
    animation: slide-in-left .5s ease-in-out forwards;
    transition: opacity .3s;
}

.slide-left-leave-active {
    animation: slide-out-left .3s ease-in-out forwards;
    transition: opacity .5s;
}
.slide-left-leave-to {
    opacity: 0;
}


.slide-right-enter {
    opacity: 0;
}
.slide-right-enter-active {
    animation: slide-in-right .5s ease-in-out forwards;
    transition: opacity .3s;
}

.slide-right-leave-active {
    animation: slide-out-right .3s ease-in-out forwards;
    transition: opacity .5s;
}
.slide-right-leave-to {
    opacity: 0;
}


@keyframes slide-in-left {
    from {
        transform: translateX(-2rem)
    }
    50% {
        transform: translateX(.5rem)
    }
    to {
        transform: translateX(0)
    }
}

@keyframes slide-out-left {
    from {
        transform: translateX(0rem)
    }
    50% {
        transform: translateX(.5rem)
    }
    to {
        transform: translateX(-2rem)
    }
}


@keyframes slide-in-right {
    from {
        transform: translateX(2rem)
    }
    50% {
        transform: translateX(-.5rem)
    }
    to {
        transform: translateX(0)
    }
}

@keyframes slide-out-right {
    from {
        transform: translateX(0rem)
    }
    50% {
        transform: translateX(-.5rem)
    }
    to {
        transform: translateX(2rem)
    }
}

</style>
