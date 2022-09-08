<script setup>
  import { ref } from 'vue';

  const currentDate = new Date().getTime()
  const targetDate = new Date("Oct 23, 2022 00:00:00").getTime()
  const distance = ref(targetDate-currentDate)
  const day = ref(Math.floor(distance.value / (1000 * 60 * 60 * 24)))
  const hour = ref(Math.floor((distance.value % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60)))
  const minutes =  ref(Math.floor((distance.value % (1000 * 60 * 60)) / (1000 * 60)))
  const seconds = ref(Math.floor(Math.floor((distance.value % (1000 * 60)) / 1000)))
  const isFinished = ref(false)

  const countdownLogic = () => {

    if(!isFinished.value){
      seconds.value--
      if(seconds.value === -1) seconds.value = 60
      else if(seconds.value === 0) {
        if(minutes.value < 0.5){ 
          setTimeout(() => {
            minutes.value = 59
            hour.value--
            if(hour.value < 0) {
              hour.value = 23
              day.value--
              if(day.value < 0) return
            }
          }, 1000)
        }
        else minutes.value--
      }
      if(seconds.value == 0 && minutes.value == 0 && hour.value == 0  && day.value == 0) isFinished.value = true
    }
    else return

  }

  setInterval(countdownLogic, 1000)


</script>

<template>
  <div class="container">
    <div class="content" v-if="!isFinished">
      <h1 class="title" >EMIR'S BIRTHDAY</h1>
      <div class="countdown" >
        <div class="single-number">
          <h1 class="number">{{day}}</h1>
          <p class="time-part">DAYS</p>
        </div>
        <div class="single-number">
          <h1 class="number">{{hour < 10 ? '0' + hour : hour}}</h1>
          <p class="time-part">HOURS</p>
        </div>
        <div class="single-number">
          <h1 class="number">{{minutes < 10 ? '0' + minutes : minutes}}</h1>
          <p class="time-part">MINUTES</p>
        </div>
        <div class="single-number">
          <h1 class="number">{{seconds < 10 ? '0' + seconds : seconds}}</h1>
          <p class="time-part">SECONDS</p>
        </div>
      </div>
    </div>
    <h1 v-if="isFinished">THERE YOU GO</h1>
  </div>
</template>

<style scoped>
.container{
  width: 100%;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  align-items: center;
  color: rgb(252, 118, 212);
}
.content{
  display: flex;
  flex-direction: column;
  align-items: center;
}
.countdown{
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}
.single-number{
  display: flex;
  flex-direction: column;
  align-items: center;
}
.number{
  width: 200px;
  height: 200px;
  margin: 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  border-radius: 10px;
  background: linear-gradient(to top, rgb(48, 44, 70) 0%, rgb(48, 44, 70) 46%, rgb(23, 20, 44) 0%, rgb(48, 44, 70) 100%);;
  font-size: 80px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}
.time-part{
  font-weight: 600;
}
@media screen and (max-width: 1050px) {
  .countdown{
    flex-direction: column;
  }
  .number{
    width: 80px;
    height: 80px;
    font-size: 30px;
  }
}

</style>
