<script>
export default {
    props: {
        risposte: {
            type: Array,
            required: true
        },
    },
    methods: {
        selezionaRisposta(risposta) {
            this.$emit('sceltaRisposta', risposta);
        }
    }
};
</script>

<template>
    <h3>Risposte</h3>
    <div>
        <button v-for="risposta in risposte" :key="risposta" @click="selezionaRisposta(risposta)">
            {{ risposta }}
        </button>
    </div>
</template>

<style scoped></style>