<script>
import {defineComponent} from 'vue'
import Elevator from "./Elevator.vue";

export default defineComponent({
  name: "Mine",
  props: ['elevator', 'countFloors'],
  components: {Elevator},


  data() {
    return {

    }
  },

  mounted() {
    // Настраиваем высоту шахты
    document.querySelector(".Mine").style.height = 100 * this.countFloors + 'px';
  },


})
</script>

<template>
  <div class="Mine">
    <Elevator :elevator.sync="elevator" :countFloors="countFloors"></Elevator>
  </div>
</template>

<style scoped>
.Mine {
  width: 100px;
  margin-right: 10px;
  border-left: 3px solid #d9dad9;
  border-right: 3px solid #d9dad9;
}
</style>