
<script setup>
    import { programaTreino } from '../utils';
    
    defineProps({
        handleSelectedWorkout: Function,
        firstIncompleteWorkoutIndex: Number,
        handleResetPlan: Function
    })

    const workoutType = ['Push', 'Pull', 'Legs']

</script>

<template>
    <section id="grid">
        <button :disabled="index > 0 && index > firstIncompleteWorkoutIndex " @click="() => handleSelectedWorkout(index)" v-for="value,index in Object.keys(programaTreino)" :key="index" class ="card-button plan-card">
            <div>
                <p>Day {{ index + 1 }}</p>
                <i class = "fa-solid fa-dumbbell" v-if="index % 3 ==0"></i>
                <i class = "fa-solid fa-weight-hanging" v-if="index % 3 ==1"></i>
                <i class = "fa-solid fa-bolt" v-if="index % 3 ==2"></i>
            </div>
            <h3>{{ workoutType[index % 3] }}</h3>
        </button>
        <button :disabled="firstIncompleteWorkoutIndex != -1" @click="handleResetPlan" class="card-button plan-card-reset">
            <p>Reset</p>
            <i class="fa-solid fa-rotate-right"></i>
        </button>
    </section>
</template>


<style scoped>
    #grid {
        display: grid;
        grid-template-columns: repeat(3, minmax(0,1fr));
        gap: 1rem;
    }

    #grid button {
        width: 100%;
    }

    #grid button:disabled{
        box-shadow: none;
        cursor: not-allowed;
    }

    .plan-card{
        display: flex;
        flex-direction: column;
    }

    .plan-card-reset {
        display: flex;
        align-items: center;
        justify-content: center;
        gap: 1rem;
    }

    .plan-card div{
        display: flex;
        align-items: center;
        justify-content: space-between;
        gap: 0.5rem;
    }
    .plan-card div p{
        text-align: left;
    }

    @media(min-width: 640px){
        #grid{
            grid-template-columns: repeat(4, minmax(0,1fr));
        }
    }
</style>
