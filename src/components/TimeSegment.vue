<script setup>
    defineProps(['number', 'segmentName'])
</script>

<template>
    <div class="time-segment">
      <h1 class="number">{{number}}</h1>
      <p class="time-part">{{segmentName}}</p>
    </div>
</template>

<style scoped>
    .time-segment{
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
        .number{
            width: 80px;
            height: 80px;
            font-size: 30px;
        }
    }
</style>