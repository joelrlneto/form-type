<template>
    <div>
        <h3>{{ questao.titulo }}</h3>
        <textarea v-model="resposta" @keyup="atualizarResposta"></textarea>
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
