<script setup>
  import Title from './components/Title.vue';
  import DatePicker from './components/DatePicker.vue';
  import TimeSegment from './components/TimeSegment.vue';
  import { ref } from 'vue';

  const isDateSet = ref(false)
  const currentDate = ref(new Date())
  const targetDate = ref(new Date())
  const targetDateR = ref(new Date())
  const distance = ref(0)
  const isFinished = ref(false)
  const day = ref(0)
  const hour = ref(0)
  const minutes =  ref(0)
  const seconds = ref(0)
  
  const setDate = (date) => {
    currentDate.value = new Date().getTime()
    targetDate.value = new Date(date).getTime()
    targetDateR.value = date
    distance.value = targetDate.value - currentDate.value
    isDateSet.value = true
    day.value = Math.floor(distance.value / (1000 * 60 * 60 * 24))
    hour.value = Math.floor((distance.value % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60))
    minutes.value =  Math.floor((distance.value % (1000 * 60 * 60)) / (1000 * 60))
    seconds.value = Math.floor(Math.floor((distance.value % (1000 * 60)) / 1000))
    setInterval(countdownLogic, 1000)
  }

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
        else setTimeout(() => {minutes.value--},1000)
      }
      if(seconds.value == 0 && minutes.value == 0 && hour.value == 0  && day.value == 0) isFinished.value = true
    }
    else return
  }

</script>

<template>
  <div class="container">
    <DatePicker @passDate="setDate" v-if="!isDateSet" />
    <div class="content" v-if="!isFinished && isDateSet">
      <Title :title="targetDateR" />
      <div class="countdown" >
        <TimeSegment :number="day" segmentName="DAYS" />
        <TimeSegment :number="hour < 10 ? '0' + hour : hour" segmentName="HOURS" />
        <TimeSegment :number="minutes < 10 ? '0' + minutes : minutes" segmentName="MINUTES" />
        <TimeSegment :number="seconds < 10 ? '0' + seconds : seconds" segmentName="SECONDS" />
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
@media screen and (max-width: 1050px) {
  .countdown{
    flex-direction: column;
  }
}

</style>
