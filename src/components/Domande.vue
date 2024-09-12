<template>
    <!-- Visualizza la domanda passata dal genitore -->
    <div class="question">
        <h1>{{ domanda }}</h1>
    </div>
</template>

<script>
export default {
    props: {
        domanda: {
            type: String,
            required: true // 'domanda' è obbligatorio
        }
    }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.question {
    padding: 1rem 0;
}
</style>
