<template>
  <div class="boxes">
    <h4 class="mb-3">Javascript Animations</h4>

    <button 
      class="btn btn-success" 
      @click="loaded = !loaded"
      >Load / Remove Element
    </button>
    <hr>
    <div class="flexbox-space-evenly flex-vert">
      <box 
        :loaded="loaded" 
        :variant="'box--box1'"
        :text="'Hello from inside the Box!'">
      </box>
      <box 
        :loaded="loaded" 
        :variant="'box--box2'"
        :text="'Animation in Vue is sweet!'">
      </box>
      <box 
        :loaded="loaded" 
        :variant="'box--box3'"
        :text="'This calls for a celebration!'">
      </box>
    </div>
    
  </div>
</template>

<script>
import Box from './Box.vue'

export default {
  data () {
    return {
      loaded: false,
    }
  },
  components: {
    'box': Box
  }
}
</script>

<style>
.boxes {
  width: 100%;
}
</style>
