<template>
    <div>
        <label class="titulo-questao">{{ questao.titulo }}</label>
        <ul class="lista-opcoes">
            <li v-for="opcao in questao.opcoes" v-bind:key="opcao.id">
                <input type="checkbox" :value="opcao.texto"
                                       @change="atualizarResposta"
                                       v-model="resposta"/> {{opcao.texto}}
            </li>
        </ul>
    </div>
</template>

<script>
export default {
  props: ["questao"],
  data(){
      return {
          resposta : []
      }
  },
  methods : {
      atualizarResposta(){
          this.$emit("respostaAtualizada", this.resposta.join(","));
      }
  }
}
</script>