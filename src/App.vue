<script setup>
  import { ref } from 'vue';

  const isDateSet = ref(false)
  const selectedDate = ref('')
  const currentDate = ref(new Date())
  const targetDate = ref(new Date())
  const distance = ref(0)
  
  const setDate = () => {
    currentDate.value = new Date().getTime()
    targetDate.value = new Date(selectedDate.value).getTime()
    distance.value = targetDate.value - currentDate.value
    isDateSet.value = true
  }

  
  const isFinished = ref(false)
  const day = ref(0)
  const hour = ref(0)
  const minutes =  ref(0)
  const seconds = ref(0)


  const countdownLogic = () => {

    day.value = ref(Math.floor(distance.value / (1000 * 60 * 60 * 24)))
    hour.value = ref(Math.floor((distance.value % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60)))
    minutes.value =  ref(Math.floor((distance.value % (1000 * 60 * 60)) / (1000 * 60)))
    seconds.value = ref(Math.floor(Math.floor((distance.value % (1000 * 60)) / 1000)))

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
        else setTimeout(() => {minutes.value--},1000)
      }
      if(seconds.value == 0 && minutes.value == 0 && hour.value == 0  && day.value == 0) isFinished.value = true
    }
    else return

  }

  setInterval(countdownLogic, 1000)


</script>

<template>
  <div class="container">
    <div class="set-date" v-if="!isDateSet">
      <p style="font-size: 2rem;">Pick your date</p>
      <input type="date" v-model="selectedDate" v-if="!isDateSet">
      <button @click="setDate">Set date</button>
    </div>
    <div class="content" v-if="!isFinished && isDateSet">
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
  color: rgb(97, 184, 255);
}
.set-date{
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2rem;
}
input{
  padding: 3rem;
  border: 0;
  border-radius: 2rem;
  background-color: rgb(21, 81, 86);
  color: rgb(97,185,255);
  font-size: 3rem;
  outline: none;
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
  font-size: 80px;
  background-color: rgb(21, 81, 86);
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
