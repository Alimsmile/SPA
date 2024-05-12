<script>


import Mine from "../components/Mine.vue";
import Floor from "../components/Floor.vue";

export default {
  components: {Mine, Floor},




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
        }/*,
        {
          status: 0,   // состояние
          position: 2, // положение
          //Очередь вызовов
          listChallenges: [],
        }*/
      ],
      // Этажи
      floors: [
        {
          number: 1,
          isActive: 0, // признак того, что на этаже есть лифт или вызов добавлен в очередь
        },
        {
          number: 2,
          isActive: 0, // признак того, что на этаже есть лифт или вызов добавлен в очередь
        },
        {
          number: 3,
          isActive: 0, // признак того, что на этаже есть лифт или вызов добавлен в очередь
        },
        {
          number: 4,
          isActive: 0, // признак того, что на этаже есть лифт или вызов добавлен в очередь
        },
        {
          number: 5,
          isActive: 0, // признак того, что на этаже есть лифт или вызов добавлен в очередь
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
    // Вызвать лифт
    callElevator(floor) {
      /*console.log("ВЫЗВАЛ")*/

      // код который определит более подходящий лифт ??

      // Если лифт находится на данном этаже
      if (this.elevators[0].position == floor.number) {
        /*console.log("лифта уже здесь")*/
        return;
      }

      // Добавить вызов в очередь (вызвать функцию дочернего компонента)
      floor = this.$refs.Mine.addToList(floor)
      // поменять признак floor по результату отработки
    },

  },


}
</script>


<template>
  <div class="spa">


    <!-- Шахты -->
<!--    <template v-for="elevator in elevators" :elevator="elevator">

    </template>-->
    <Mine :key="elevators.id" :elevator.sync="elevators[0]" :floors.sync="floors" ref="Mine"></Mine>


    <!-- Этажи -->
    <div class="floors" :style="{'height': 100 * floors.length + 'px'}">
      <template v-for="floor in floors" :floor="floor">
        <Floor :floor.sync="floor" :callElevator="callElevator"></Floor>
      </template>
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
      flex-direction: column-reverse;
      justify-content: space-evenly;
    }
  }

</style>

