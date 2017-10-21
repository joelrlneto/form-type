<template>
    <div class="bloco-questao">
        <questaoTextoSimples v-if="questao.tipo == 'texto-simples'"
                             :questao="questao"
                             @respostaAtualizada="respostaAtualizada"/>

        <questaoTextoLongo v-if="questao.tipo == 'texto-longo'"
                           :questao="questao"
                           @respostaAtualizada="respostaAtualizada"/>

        <questaoRadiobutton v-if="questao.tipo == 'radio'"
                            :questao="questao"
                            @respostaAtualizada="respostaAtualizada"/>

        <questaoCheckbox v-if="questao.tipo == 'check'"
                         :questao="questao"
                         @respostaAtualizada="respostaAtualizada"/>
    </div>
</template>

<script>
import questaoTextoSimples from './QuestaoTextoSimples.vue';
import questaoTextoLongo from './QuestaoTextoLongo.vue';
import questaoCheckbox from './QuestaoCheckbox.vue';
import questaoRadiobutton from './QuestaoRadiobutton.vue';

export default {
    components : { questaoTextoSimples, questaoTextoLongo, questaoCheckbox, questaoRadiobutton },
    props: ["questao"],
    methods : {
        respostaAtualizada(resposta){
            this.$emit("questaoRespondida", this.questao.id, resposta);
        }
    }
}
</script>

<style>
.bloco-questao{
    min-height:200px;
}
</style>