<template>
  <div class="app">
    <div class="conteudo">
      <transition name="fade">
        <cabecalho :titulo="titulo"
                   :subtitulo="subtitulo"
                   v-if="questaoAtual == 0"/>
      </transition>

      <transition name="fade">
        <questao v-for="questao in questoes"
                 :questao="questao"
                 :key="questao.id"
                 v-if="questao.id == questaoAtual"
                 @questaoRespondida="questaoRespondida"/>
      </transition> 

      <transition name="fade">
        <finalizacao :mensagem="mensagemFinal"
                     :url="urlFinalizacao"
                     v-if="questaoAtual == totalQuestoes + 1"/>
      </transition>
    </div>
  
    <div class="acoes">
      <div class="bloco-botoes">
        <button class="button" @click="voltar" v-if="questaoAtual > 0">Voltar</button>
        <button class="button" @click="avancar" v-if="questaoAtual <= totalQuestoes">Avançar</button>
        <button class="button" @click="finalizar" v-if="questaoAtual == totalQuestoes + 1">Finalizar</button>
      </div>
    </div>

    <footer class="rodape" v-if="questaoAtual > 0 && questaoAtual <= totalQuestoes">
      <p>Questão {{questaoAtual}} de {{ totalQuestoes }}</p>
    </footer>
  </div>
</template>

<script>
import cabecalho from './Cabecalho.vue';
import questao from './Questao.vue';
import finalizacao from './Finalizacao.vue';

var dados = {
  titulo: "",
  subtitulo: "",
  questoes: [],
  questaoAtual : 0,
  totalQuestoes: 0,
  mensagemFinal : "",
  urlFinalizacao:"",
  respostas : []
};

fetch("/form.json").then(form => {
  form.json().then(json => {
    dados.titulo = json.cabecalho.titulo;
    dados.subtitulo = json.cabecalho.subtitulo;
    dados.questoes = json.questoes;
    dados.totalQuestoes = json.questoes.length;
    dados.mensagemFinal = json.finalizacao.mensagem;
    dados.urlFinalizacao = json.finalizacao.url
  });
});

export default {
  components: { cabecalho, questao, finalizacao },
  data() {
    return dados;
  },
  methods : {
    avancar(){
      if(this.questaoAtual <= this.totalQuestoes){
        this.questaoAtual++;
      }
    },
    voltar(){
      if(this.questaoAtual > 0){
        this.questaoAtual--;
      }
    },
    finalizar(){
      var respostasFinais = this.respostas.map((item, indice) => `"${indice}":"${item}"`);
      document.write("RESPOSTAS: <pre>", `{${respostasFinais.join(" , ")}}`);
    },
    questaoRespondida(id, resposta){
      this.respostas[id-1] = resposta;
    }
  }
}
</script>

<style>
.container{
      width: 100%;
      height: 100%;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
}
.fade-enter-active {
  transition: opacity 1s
}
.fade-enter,.fade-leave-to, .fade-leave {
  opacity: 0
}
</style>