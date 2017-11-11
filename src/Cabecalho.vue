<template>
    <div class="cabecalho">
        <h1>{{ titulo }}</h1>
        <h2>{{ subtitulo }}</h2>
    </div>
</template>

<script>
export default {
    props:["titulo", "subtitulo"],
    methods : {
        avancar(){
            alert("Avançar para a próxima questão");
        }
    }
}
</script>