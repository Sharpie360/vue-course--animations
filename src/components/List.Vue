<template>
  <div>
    <div class="card">
      <h5 class="card-header">Animation with Vue</h5>
      <div class="card-body expand-body p-0">
        <ul class="list-group list-group-flush">
          <transition-group name="slide-left">
            <li
              class="list-group-item"
              v-for="(item, i) in list"
              :key="i"
              @click="removeItem(i)"
              >{{ i + 1 }}. {{ item }}
            </li>
          </transition-group>
        </ul>
      </div>
      <div class="card-action">
        <button 
          @click="addItem"
          class="btn btn-primary mt-3 mr-2"
          >Add
        </button>
        <button 
          @click="removeItem"
          class="btn btn-danger mt-3"
          >Remove
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      list: [
        'Some fancy list items here. Number 0',
        'Some fancy list items here. Number 1',
        'Some fancy list items here. Number 2',
      ]
    }
  },
  methods: {
    addItem() {
      const newItem = Math.floor(Math.random() * this.list.length)
      console.log(newItem)
      this.list.splice(newItem, 0, `Some fancy list items here. Number ${this.list.length}`)
    },
    removeItem(i) {
      this.list.splice(i, 1)
    
    }
  }
}
</script>

<style>
.card {
  background-color: transparent;
}
.card-header {
  color: #03a9ac;
  background-color: rgba(255, 255, 255, 0.9);
}
.card-body {
  color: #4b4b4b;
}


</style>
