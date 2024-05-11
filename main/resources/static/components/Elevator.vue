<script>
import {defineComponent} from 'vue'

export default defineComponent({
  name: "Elevator",
  props: ['elevator', 'countFloors'],


  mounted() {
  },


})
</script>

<template>
  <div class="Elevator" :style="{'top': (countFloors - elevator.position) * 100  + 'px'}">

  </div>
</template>

<style scoped>
.Elevator {
  width: 100px;
  height: 100px;
  background-color: #00fdfe;
  position: relative;
}
</style>