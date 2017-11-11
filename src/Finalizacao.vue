<template>
  <div class="columns">
      <h2 class="title">{{ mensagem }}</h2>
  </div>
</template>

<script>
export default {
  props : ["mensagem", "url"]
}
</script>