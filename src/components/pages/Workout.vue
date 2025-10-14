<script setup>
    import { programaTreino, descricoesExercicios } from '../../utils';
    import ModalPortal from '../ModalPortal.vue';
    import { ref } from 'vue'

    let modal = ref(false);
    const selectedWorkout = 4;
    const { treino, aquecimento } = programaTreino[selectedWorkout];
    const selectedExercises = 'Rosca direta no cabo';
    const exerciseDescriptions = descricoesExercicios[selectedExercises];
    const openModal = () => modal.value = true;
    
</script>

<template>
<section id="workout-card">
    <ModalPortal v-if="modal">
        <div class="exercise-descriptions">
            <h4> {{ selectedExercises }}</h4>
            <div>
                <small>Descrição</small>
                <p>{{ exerciseDescriptions }}</p>
            </div>
            <button>Exit <i class ="fa-solid fa-xmark"></i></button>
        </div>
    </ModalPortal>
    <div class ="plan-card card">
        <div class =plan-card-header>
            <p>Day {{ selectedWorkout < 9 ? '0' + selectedWorkout : selectedWorkout }}</p>
            <i class="fa-solid fa-dumbbell"></i>
        </div>
        <h2>{{ 'Push' }} Workout</h2>
    </div>

    <div class="workout-grid">
        <h4 class="grid-name">Warmup</h4>
        <h6>Sets</h6>
        <h6>Reps</h6>
        <h6 class ="grid-weights">Weights</h6>
        <div class="workout-grid-row" v-for="(w,wId) in aquecimento" :key="wId">
           <div class ="grid-name">
                <p>{{ w.nome }}</p>
                <button @click="openModal"><i class="fa-regular fa-circle-question"></i></button>
            </div>
            <p>{{ w.series }}</p>
            <p>{{ w.repeticoes }}</p>
            <input class="grid-weights" placeholder="14kg" type="text" disabled>
        </div>
        <!---->
        <div class="workout-grid-line"></div>
        <!---->
        <h4 class="grid-name">Workout</h4>
        <h6>Sets</h6>
        <h6>Reps</h6>
        <h6 class ="grid-weights">Weights</h6>
        <div class="workout-grid-row" v-for="(w,wId) in treino" :key="wId">
           <div class ="grid-name">
                <p>{{ w.nome }}</p>
                <button @click="openModal"><i class="fa-regular fa-circle-question"></i></button>
            </div>
            <p>{{ w.series }}</p>
            <p>{{ w.repeticoes }}</p>
            <input class="grid-weights" placeholder="14kg" type="text" >
        </div>
    </div>
    <div class="card workout-btn">
        <button> Save & Exit <i class="fa-solid fa-save"></i></button>
        <button> Complete <i class="fa-solid fa-check"></i></button>
    </div>
</section>
</template>



<style scoped>
    #workout-card,
    .plan-card{
        display: flex;
        flex-direction: column;
    }
    #workout-card{
        gap: 1.5rem;
    }

    .plan-card-header,
    .workout-btn{
        display: flex;
        align-items: center;
        justify-content: space-between;
        gap: 1rem;
    }

    .workout-grid,
    .workout-grid-row{
        display: grid;
        grid-template-columns: repeat(7,minmax(0,1fr));
        gap: 1rem;
    }

    .workout-grid-row,
    .workout-grid-line{
        grid-column: span 7 / span 7;
    }

    .grid-name{
        grid-column: span 3 / span 3;
        display: flex;
        align-items: center;
        gap: 1rem;
    }
    .grid-name button {
        padding: 0;
        border: none;
        box-shadow: none;
    }

    .grid-name button:hover{
        transform: none;
        box-shadow: none;
        color: var(--color-link)
    }

    .workout-grid-row .grid-name button{
        opacity: 0;
        pointer-events: none;  
    }
    .workout-grid-row:hover .grid-name button{
        opacity: 1;
        pointer-events: all;
    }

    .grip-name p {
        text-transform: capitalize;
    }
    .grid-weights{
        grid-column: span 2 / span 2;  
    }
    
    .workout-btn button{
        flex:1;
    }
     .workout-btn button i{
        padding-left: 1rem;
    }

    .exercise-descriptions{
        display: flex;
        flex-direction: column;
        gap: 1rem;
    }
    .exercise-descriptions button i {
        padding-left: 0.5rem;
    }
</style>
