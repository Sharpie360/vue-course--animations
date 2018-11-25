<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <h1>Animations</h1>
                <hr>
                <button class="btn btn-primary mb-3" @click="show = !show">Show Alert</button>
                <transition name="fade">
                    <div class="alert alert-info" v-if="show">This is an alert box!</div> 
                </transition>
                <transition name="slide">
                    <div class="alert alert-info" v-if="show">This is an alert box!</div> 
                </transition>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                show: false
            }
        }
    }
</script>

<style>

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

.slide-enter {
    opacity: 0;
}
.slide-enter-active {
    animation: slide-in .5s ease-in-out forwards;
    transition: opacity .3s;
}

.slide-leave-active {
    animation: slide-out .3s ease-in-out forwards;
    transition: opacity .5s;
}
.slide-leave-to {
    opacity: 0;
}

@keyframes slide-in {
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

@keyframes slide-out {
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

</style>
