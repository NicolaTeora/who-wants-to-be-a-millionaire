<script>
export default {
    data() {
        return {
            rispostaSelezionata: null // Variabile per tracciare la risposta selezionata
        };
    },
    watch: {
        // Ogni volta che cambia la lista delle risposte, resetta la selezione
        risposte() {
            this.rispostaSelezionata = null;
        }
    },
    props: {
        risposte: {
            type: Array,
            required: true
        },
        rispostaCorretta: {
            type: String,
            required: true
        }
    },
    methods: {
        selezionaRisposta(risposta) {
            // Imposta la risposta selezionata
            this.rispostaSelezionata = risposta;
            // Emetti la risposta selezionata al componente genitore
            this.$emit('selezionaRisposta', risposta);
        }
    }
};
</script>

<template>
    <div class="risposte">
        <button class="risposta" v-for="risposta in risposte" :key="risposta" @click="selezionaRisposta(risposta)"
            :class="{ 'corretta': rispostaSelezionata === risposta && risposta === rispostaCorretta, 'sbagliata': rispostaSelezionata === risposta && risposta !== rispostaCorretta }"
            :disabled="rispostaSelezionata !== null">
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
    transition: background-color 0.3s ease;
}

/* Cambia il colore del pulsante se la risposta è corretta */
.risposta.corretta {
    background-color: green;
    color: white;
}

/* Cambia il colore del pulsante se la risposta è sbagliata */
.risposta.sbagliata {
    background-color: red;
    color: white;
}
</style>