<template>
    <div class="teclado">

        <button class="teclado-botao" v-for="(letra, key) in 'abcdefghijklmnopqrstuvwxyz'" :key="key"
            :disable="verificaLetra(letra)" v-on:click="jogar(letra)">{{ letra }}

        </button>

    </div>
</template>

<script>


export default {
    name: 'tecladoDefault',
    props: {
        letras: Array,
        verificaLetra: Function,
        jogar: Function

    },
    data() {
        return {

        }
    },
    methods: {

    },
    components: {

    },
}
</script>

<style scoped>
.teclado {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    max-width: 80%;
    margin-top: 20px;
}

.teclado-botao {
    margin: 5px;
    text-transform: uppercase;
}
</style>