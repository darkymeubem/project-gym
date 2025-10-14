<script setup>
    import { programaTreino } from '../../utils';
    console.log(programaTreino);
    const selectedWorkout = 4;
    const { treino, aquecimento } = programaTreino[selectedWorkout];
</script>

<template>
<section id="workout-card">
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
                <button><i class="fa-regular fa-circle-question"></i></button>
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
                <button><i class="fa-regular fa-circle-question"></i></button>
            </div>
            <p>{{ w.series }}</p>
            <p>{{ w.repeticoes }}</p>
            <input class="grid-weights" placeholder="14kg" type="text" >
        </div>
    </div>
    <div class="card">
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

    .plan-card-header{
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
</style>
