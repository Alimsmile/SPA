<script>
import {defineComponent} from 'vue'

export default defineComponent({
  name: "Elevator",
  props: ['elevator', 'floors'],


  data() {
    return {
    }
  },


  mounted() {
    if (this.elevator.listChallenges.length) {
      this.executeListChallenges();
    }
  },


  methods: {
    // Перемещение лифта
    movElevator(currentPosition, endPosition, direction) {
      if (this.elevator.status == 0) {


        this.elevator.status = 1;
        this.elevator.position = this.elevator.listChallenges[0];

        let tempElevator = this.elevator

        let tempFloor = this.floors;

        let timer = setInterval(function() {


          if (direction) {
            currentPosition++;
          }
          else {
            currentPosition--;
          }

          /*if (this.elevator.position < this.elevator.listChallenges[0]) {
            let time = this.elevator.listChallenges[0] - this.elevator.position;
          }
          else if (this.elevator.position > this.elevator.listChallenges[0]) {
            let time = this.elevator.position - this.elevator.listChallenges[0];

          }*/


          document.querySelector(".Elevator").style.bottom = currentPosition + 'px';


          if (currentPosition == endPosition) {

            for (let i = 0 ; i < tempFloor.length; i++) {
              if (tempFloor[i].number == tempElevator.listChallenges[0]) {
                tempFloor[i].isActive = 0;
                break;
              }
            }

            clearInterval(timer);
            // Убираем первый элемент в очереди
            tempElevator.listChallenges.shift()


            // Достигнув нужного этажа лифт 3 секунды «отдыхает»
            setTimeout(() => {
              tempElevator.status = 0
            }, 3000);
          }
        }, 10);
      }
    },
    // Отработка очереди с вызовами
    executeListChallenges() {
      if (this.elevator.status) {
        console.log("вышел")
        return;
      }

      console.log("отработай очередь")
      // в отработке рекурсия, управление активностью лифта, этажа



      // тут вызываем сам метод перемещения, думаю, будем считать время, которое необходимо для перемешния здесь
      // и пускаем здесь таймер на это время и далее по очереди



      // Определяем текущее положение лифта
      let bottom = document.querySelector(".Elevator").style.bottom;
      let currentPosition = 0;
      if (bottom != "") {
        currentPosition = bottom.slice(0, bottom.length - 2)
      }
      // Позиция, которой необходимо достичь
      let endPosition = (this.elevator.listChallenges[0] - 1) * 100;
      // Время, которое будет затрчено для перемещения
      let completionTime = 0;


      // Определяем направление лифта (1 - вверх, 0 - вниз)
      let direction = 1;
      if (this.elevator.position < this.elevator.listChallenges[0]) {
        completionTime = (endPosition - currentPosition) * 10 + 3000 + 500; // 3000 - время ожидание на этаже
        direction = 1;
      }
      else if (this.elevator.position > this.elevator.listChallenges[0]) {
        completionTime = (currentPosition - endPosition) * 10 + 3000 + 500; // 3000 - время ожидание на этаже
        direction = 0;
      }
      else {
        return;
      }

      console.log(currentPosition)
      console.log(endPosition)
      console.log(direction)
      console.log(completionTime)

      // Выполнение вызовов в очереди
      this.movElevator(currentPosition, endPosition, direction);

      // Ожидаем завершения через определенное время и вызываем по рекурсий
      setTimeout(() => {
        /*console.log("круг")
        if (this.elevator.status) {
          setTimeout(() => {
            console.log("круг")
            this.executeListChallenges();
          }, 1000);
        }*/
        this.executeListChallenges();
      }, completionTime);
      //this.executeListChallenges();



      /* this.elevator.position = this.elevator.listChallenges[0];
       // Убираем первый элемент в очереди
       this.elevator.listChallenges.shift()*/


    }
  }
})
</script>

<template>
  <div class="Elevator" :style="{'bottom': (elevator.position - 1) * 100  + 'px'}" :class="{ rest: elevator.status }">
<!--    {{elevator}}-->
  </div>
</template>

<style scoped>
.Elevator {
  width: 100px;
  height: 100px;
  background-color: #00fdfe;
  position: relative;
}
.rest {
  background-color: grey;
}
</style>