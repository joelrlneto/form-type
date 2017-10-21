<template>
    <div>
        <h3>{{ questao.titulo }}</h3>
        <input type="text" v-model="resposta" @keyup="atualizarResposta">
    </div>
</template>

<script>
export default {
  props: ["questao"],
  data(){
      return {
          resposta : ""
      }
  },
  methods : {
      atualizarResposta(){
          this.$emit("respostaAtualizada", this.resposta);
      }
  }
}
</script>