<script setup>
    import { ref } from 'vue'

    const emit = defineEmits(['passDate'])
    const selectedDate = ref('')

    const passDate = () => emit('passDate', selectedDate.value)

</script>

<template>
    <div class="set-date">
        <p style="font-size: 2rem;">Pick your date</p>
        <input type="date" v-model="selectedDate">
        <button @click="passDate">Set date</button>
    </div>
</template>

<style scoped>
    .set-date{
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 2rem;
    }
    input{
        padding: 3rem;
        border: 0;
        border-radius: 1rem;
        background-color: rgb(21, 81, 86);
        color: rgb(97,185,255);
        font-size: 3rem;
        font-family: Inter, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu,
            Cantarell, 'Fira Sans', 'Droid Sans', 'Helvetica Neue', sans-serif;
        outline: none;
    }
    button{
        padding: 1rem 3rem;
        border: 0;
        border-radius: 0.5rem;
        background-color: rgb(227, 234, 235);
        color: rgb(19, 63, 99);
        font-size: 1.2rem;
        cursor: pointer;
        transition: 0.3s;
    }
    button:hover{
        scale: 1.1;
    }
</style>