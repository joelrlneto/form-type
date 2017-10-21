<template>
  <div class="bloco-finalizacao">
      <h2>{{ mensagem }}</h2>
  </div>
</template>

<script>
export default {
  props : ["mensagem", "url"]
}
</script>

<style>
.bloco-finalizacao{
    min-height:200px;
}
</style>