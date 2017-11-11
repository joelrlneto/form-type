<template>
    <div>
        <label class="titulo-questao">{{ questao.titulo }}</label>
        <textarea v-model="resposta" @keyup="atualizarResposta" class="textarea"></textarea>
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
