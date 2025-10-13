
<script setup>

</script>

<template>
    <section id="welcome">
        <div class="benefits">
            <h2>Complete esse programa<br>se voce quiser...</h2>
            <p>✅ Siga um programa simples com resultados comprovados.</p>
            <p>✅ Fique saudável, forte e com bons hábitos!</p>
            <p>✅ Aprenda mais sobre academia, treino e estilo de vida saudável.</p>
       
        </div>
        <div>
            <h3>O planejamento de treino</h3>
            <p>Esse planejamento de treino segue uma estrutura conhecida como <strong>Bro Split</strong>.</p>
            <h5>Push &rarr; Pull &rarr; Legs &rarr; Repeat</h5>
        </div>
        <div class="card challenge">
            <h3>🔥Seu Desafio</h3>
            <p>Complete todos seus exercícios e acompanhe seu progresso ao longo do caminho.</p>
            <p>Você aceita?</p>
            <button class="card-button">Comece &rarr;</button>
        </div>

    </section>
</template>


<style scoped>

    #welcome,
    .challenge,  
    .benefits{
        display: flex;
        flex-direction: column;
    }

    #welcome{

        gap: 1.5rem;
    }
    .benefits{
        gap: 0.5rem;
    }
    .challenge{
        gap: 0.25rem;
    }

    @media (min-width: 640px){
        #welcome{
            gap: 2rem;
            padding: 1rem 0
        }

        .benefits{
            gap: 1rem;
        }
    }
</style>
