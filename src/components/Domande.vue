<template>
    <!-- Visualizza la domanda passata dal genitore -->
    <h1>{{ domanda }}</h1>
</template>

<script>
export default {
    props: {
        domanda: {
            type: String, // Definisce che 'domanda' deve essere una stringa
            required: true // Indica che 'domanda' è obbligatorio
        }
    }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
