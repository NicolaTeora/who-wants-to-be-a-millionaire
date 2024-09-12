<script>
export default {
    props: {
        risposte: {
            type: Array,
            required: true
        },
        rispostaCorretta: {
            type: String,
            required: true
        },
        rispostaSelezionata: {
            type: String,
            default: ''
        }
    },
    methods: {
        selezionaRisposta(risposta) {
            this.$emit('sceltaRisposta', risposta);
        },
        getButtonClass(risposta) {
            if (this.rispostaSelezionata === risposta) {
                return this.rispostaSelezionata === this.rispostaCorretta ? 'corretto' : 'sbagliato';
            }
            return '';
        }
    }
};
</script>

<template>
    <div class="risposte">
        <button class="risposta" :class="getButtonClass(risposta)" v-for="risposta in risposte" :key="risposta"
            @click="selezionaRisposta(risposta)">
            {{ risposta }}
        </button>
    </div>
</template>

<style scoped>
.risposte {
    margin: 2rem auto;
    width: 80%;
}

.risposta {
    padding: 5px;
    width: 25%;
    border: 3px solid gray;
    border-radius: 20px;
    background-color: inherit;
}

.corretto {
    background-color: green;
    color: white;
}

.sbagliato {
    background-color: red;
    color: white;
}
</style>