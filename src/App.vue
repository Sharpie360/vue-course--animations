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
    transform: translateY(0);
    transition: all .3s ease-in-out;
}
.fade-leave-active {

}

.fade-leave-to {

}

</style>
