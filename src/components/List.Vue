<template>
  <div class="card">
    <h5 class="card-header">Animation with Vue</h5>
    <div class="card-body expand-body p-0">
      <ul class="list-group list-group-flush">
        <transition-group>
          <li
            class="list-group-item"
            v-for="(item, i) in 2"
            :key="i"
          >{{ i }}. Some fancy list items here</li>
        </transition-group>
      </ul>
    </div>
  </div>
</template>

<script>
export default {

}
</script>

<style>

</style>
