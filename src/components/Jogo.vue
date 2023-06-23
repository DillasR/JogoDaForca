<template>
    <div class="jogo">
        <forcaDefault :erros="erros" />

        <palavraDefault :palavra="palavra" :dica="dica" :verificaLetra="verificaLetra" :etapa="etapa" />


        <tecladoDefault v-if="etapa === 'jogo'" :letras="letras" :verificaLetra="verificaLetra" :jogar="jogar" />


        <finalDefault v-if="etapa != 'jogo'" :etapa="etapa" :texto="etapa === 'ganhador' ? 'Parabéns:)' : 'Tadinho :('"
            :jogarNovamente="jogarNovamente" />
    </div>
</template>

<script>
import forcaDefault from './Forca'
import palavraDefault from './Palavra'
import tecladoDefault from './Teclado'
import finalDefault from './Final'

export default {
    name: 'jogoDefault',
    props: {

        palavra: String,
        dica: String,
        erros: Number,
        verificaLetra: Function,
        etapa: String,
        letras: Array,
        jogar: Function,
        jogarNovamente: Function
    },
    data() {
        return {

        }
    },
    methods: {

    },
    components: {
        forcaDefault,
        palavraDefault,
        tecladoDefault,
        finalDefault
    },
}
</script>

<style scoped>
.jogo {
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
}
</style>