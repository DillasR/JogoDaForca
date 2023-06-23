<template>
  <div id="app">

    <h1>Jogo da forca Dev-D</h1>

    <section v-if="tela === 'inicio'" id="inicio">

      <formularioDefault v-if="etapa === 'palavra'" title="Defina a Palavra" button="Próximo" :action="setPalavra" />

      <formularioDefault v-if="etapa === 'dica'" title="Defina a Dica" button="Iniciar o jogo :)" :action="setDica" />

    </section>

    <section v-if="tela === 'jogo'" id="jogo">


      <jogoDefault :palavra="palavra" :dica="dica" :erros="erros" :verificaLetra="verificaLetra" :etapa="etapa"
        :letras="letras" :jogar="jogar" :jogarNovamente="jogarNovamente" />
    </section>



  </div>
</template>

<script>
import './assets/css/global.css'
import formularioDefault from './components/Formulario'
import jogoDefault from './components/Jogo'
export default {
  name: 'App',
  data() {
    return {
      tela: 'inicio',
      etapa: 'palavra',
      palavra: '',
      dica: '',
      erros: 0,
      letras: []

    }
  },
  components: {
    formularioDefault,
    jogoDefault
  },
  methods: {
    setPalavra: function (palavra) {
      this.palavra = palavra;
      this.etapa = 'dica';
    },
    setDica: function (dica) {
      this.dica = dica;
      this.tela = 'jogo';
      this.etapa = 'jogo';
    },
    verificaLetra: function (letra) {
      return this.letras.find(item => item.toLowerCase() === letra.toLowerCase());
    },

    jogar: function (letra) {
      //adiciona letra jogada 
      this.letras.push(letra);

      //Validar Erro
      this.verificarErros(letra);
    },
    verificarErros: function (letra) {
      //acerto
      if (this.palavra.toLowerCase().indexOf(letra.toLowerCase()) >= 0) {
        return this.verificaAcertos();
      }

      //Erros
      this.erros++;

      //enforcado
      if (this.erros === 6) {
        this.etapa = 'enforcado'
      }
    },

    verificaAcertos: function () {
      let letrasUnicas = [...new Set(this.palavra.split(''))];
      if (letrasUnicas.length === (this.letras.length - this.erros)) {
        this.etapa = 'ganhador';
      }
    },

    jogarNovamente: function () {
      this.palavra = '';
      this.dica = '';
      this.erros = 0;
      this.letras = [];
      this.tela = 'inicio';
      this.etapa = 'palavra';
    }
  }
}
</script>

<style>
#app {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

}
</style>
