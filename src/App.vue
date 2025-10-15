<script setup>
    import Welcome from './components/pages/Welcome.vue'
    import Dashboard from './components/pages/Dashboard.vue'
    import Workout from './components/pages/Workout.vue'
    import Layout from './components/layouts/Layout.vue'
    import { computed, ref } from 'vue'
    import { programaTreino } from './utils'

    const defaultData = {};
    for(let workoutIdx in programaTreino){
        const workoutData = programaTreino[workoutIdx]
        defaultData[workoutIdx] = {};

        for(let e of workoutData.treino)[
            defaultData[workoutIdx][e.nome] = ''
        ]
    }

    const selectedDisplay = ref(1);
    const data = ref(defaultData);
    const selectedWorkout = ref(-1);

    const isWorkoutComplete = computed(() => {
        const currWorkout = data.value?.[selectedWorkout.value]
        if(!currWorkout){ return false} //guard clause to exit function

        const isCompleteCheck = Object.values(currWorkout).every(ex => !!ex);
        console.log('ISCOMPLETE: ', isCompleteCheck)
        return isCompleteCheck
    })

    const firstIncompleteWorkoutIndex = computed(() =>{
        const allWorkouts = data.value;
        if(!allWorkouts){return -1}

        //loop over every key  value par, and check if the workout is complete or not
        for (const [index, workout] of Object.entries(allWorkouts)){
            const isComplete = Object.values(workout).every(ex => !!ex)
            console.log(index, workout);
            
            if(!isComplete){
                return parseInt(index);
            }
        }
        return -1 // all are complete

    })
    function handleChangeDisplay(idx){
        selectedDisplay.value = idx;
    }

    function handleSelectedWorkout(idx){
        selectedDisplay.value = 3;
        selectedWorkout.value = idx;
    }

    function handleSaveWorkout(){
        // save the current data snapshot to localStorage
        localStorage.setItem('workoutData', JSON.stringify(data.value));
        //show the dashboard
        selectedDisplay.value = 2;
        //deselect a workout
        selectedWorkout.value = -1;

    }
</script>

<template>
    <Layout>
        <!-- PAGE 1 -->
        <Welcome :handleChangeDisplay="handleChangeDisplay" v-if="selectedDisplay == 1"/>
        <!-- PAGE 2 -->
        <Dashboard :handleSelectedWorkout="handleSelectedWorkout" v-if="selectedDisplay == 2"/>
        <!-- PAGE 3 -->
        <Workout :handleSaveWorkout="handleSaveWorkout" :data="data" :selectedWorkout="selectedWorkout" :isWorkoutComplete="isWorkoutComplete" v-if="programaTreino?.[selectedWorkout]"/>
    </Layout>
</template>

<style scoped>

</style>
