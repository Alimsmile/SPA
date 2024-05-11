<script>


import Mine from "../components/Mine.vue";

export default {
  components: {Mine},


  data() {
    return {
      // Лифты
      elevators: [
        {
          status: 0,   // состояние
          position: 1, // положение
          /* Очередь вызовов
          {
            floorNum: 0, // номер этажа
          }
          */
          listChallenges: [],
        },
        {
          status: 0,   // состояние
          position: 2, // положение
          //Очередь вызовов
          listChallenges: [],
        }
      ],

      // Количество этажей
      countFloors: 5,
    }
  },


  mounted() {

  },


  beforeDestroy() {

  },


  methods: {
  },


}
</script>


<template>
  <div class="spa">


    <!-- Шахты -->
    <Mine v-for="elevator in elevators" :key="elevator.id" :elevator.sync="elevator" :countFloors="countFloors"></Mine>


    <!-- Этажи -->
    <div class="floors" :style="{'height': 100 * countFloors + 'px'}">
      <div class="floor" v-for="floor in countFloors" :floor="floor">
        {{countFloors - floor + 1}}
        <button>⦿</button>
      </div>
    </div>


  </div>
</template>


<style>
.spa {
  display: flex;
  padding: 10px;
  border-top: 5px solid #373736;
  border-bottom: 5px solid #373736;




  .floors {
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;

    .floor {
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
    }

  }


}
</style>

