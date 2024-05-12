<script>
import {defineComponent} from 'vue'

export default defineComponent({
  name: "Floor",
  props: ['floor', 'callElevator'],


  methods: {
    // Нажать кнопку вызова лифта
    clickButton() {
      // Если на этаже уже есть лифт или вызов добавлен в очередь
      if (this.floor.isActive) {
       /* console.log("На этаже есть лифт или вызов был осуществлен и добавлен в очередь")*/
        return;
      }

      // Вызвать лифт
      this.callElevator(this.floor);
    },
  },


})
</script>

<template>
  <div class="Floor">
    {{floor.number}}
    <button :class="{ active: floor.isActive }" @click="clickButton()">⦿</button>
  </div>
</template>

<style scoped>
  .Floor {
    display: flex;
    flex-direction: column;
    height: 100px;
    button {
      margin-top: 10px;
      padding: 3px;
      background-color: white;
      border: 1px solid #02969e;
      border-radius: 5px;
      color: #02969e;
    }
    button:hover {
      background-color: rgba(229, 226, 226, 0.99);
    }
    button:active {
      background-color: #b2cbe1;
      color: white;
    }
    .active {
      border: 1px solid red;
      color: red;
    }
  }
</style>