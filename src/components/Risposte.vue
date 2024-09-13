<script>
export default {
    props: {
        risposte: {
            type: Array,
            required: true
        }
    },
    methods: {
        selezionaRisposta(risposta) {
            this.$emit('selezionaRisposta', risposta);
        }
    }
};
</script>

<template>
    <div class="risposte">
        <button class="risposta" v-for="risposta in risposte" :key="risposta" @click="selezionaRisposta(risposta)">
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
</style>