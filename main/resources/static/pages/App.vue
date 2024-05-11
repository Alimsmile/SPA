<script>


export default {


  components: {},


  data() {
    return {
      // Лифты
      elevators: [
        {
          status: 0,   // состояние
          position: 1, // положение
        },
        {
          status: 0,   // состояние
          position: 3, // положение
        }
      ],
      /* Очередь вызовов
        {
          floorNum: 0, // номер этажа
        }
       */
      listChallenges: [],
      // Этажи
      floors: [1, 2, 3, 4, 5],
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
    <div class="mine" v-for="mine in elevators" :mine="mine" :style="{'height': 100 * floors.length + 'px'}">
      <div class="elevator" :style="{'top': (floors.length - mine.position) * 100  + 'px'}">{{mine.position}}</div>
    </div>


    <!-- Этажи -->
    <div class="floors" :style="{'height': 100 * floors.length + 'px'}">
      <div class="floor" v-for="floor in floors" :floor="floor">
        {{floors.length - floor + 1}}
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


  .mine {
    width: 100px;
    margin-right: 10px;
    border-left: 3px solid #d9dad9;
    border-right: 3px solid #d9dad9;

    .elevator {
      width: 100px;
      height: 100px;
      background-color: #00fdfe;
      position: relative;
    }

  }


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

