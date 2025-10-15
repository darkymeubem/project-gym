<script setup>
    import Welcome from './components/pages/Welcome.vue'
    import Dashboard from './components/pages/Dashboard.vue'
    import Workout from './components/pages/Workout.vue'
    import Layout from './components/layouts/Layout.vue'
    import { ref } from 'vue'
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
        <Welcome v-if="selectedDisplay == 1"/>
        <!-- PAGE 2 -->
        <Dashboard v-if="selectedDisplay == 2"/>
        <!-- PAGE 3 -->
        <Workout :data="data" :selectedWorkout="selectedWorkout" v-if="programaTreino?.[selectedWorkout] "/>
    </Layout>
</template>

<style scoped>

</style>
