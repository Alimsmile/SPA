<script>
import {defineComponent} from 'vue'
import Elevator from "./Elevator.vue";

export default {
  name: "Mine",
  props: ['elevator', 'floors'],
  components: {Elevator},

  mounted() {
    // Настраиваем высоту шахты
    document.querySelector(".Mine").style.height = 100 * this.floors.length + 'px';
  },


  methods: {
    // Добавить вызов лифта в очередь
    addToList(floor) {
      /*console.log("ДОБАВИЛ В ОЧЕРЕДЬ")*/
      // Если очередь вызовов был пуст, вызвать функцию отработки списка
      if (!this.elevator.listChallenges.length) {
        this.elevator.listChallenges.push(floor.number);
        this.$refs.Elevator.executeListChallenges()
      }
      else {
        this.elevator.listChallenges.push(floor.number);
      }

      // Возвращаем результат, чтобы повторно не добавлять вызов в очередь
      floor.isActive = 1;
      return floor;
    },
  },


}
</script>

<template>
  <div class="Mine">
    <Elevator :elevator.sync="elevator" :floors.sync="floors" ref="Elevator"></Elevator>
  </div>
</template>

<style scoped>
.Mine {
  display: flex;
  flex-direction: column;
  justify-content: end;
  width: 100px;
  margin-right: 10px;
  border-left: 3px solid #d9dad9;
  border-right: 3px solid #d9dad9;
}
</style>