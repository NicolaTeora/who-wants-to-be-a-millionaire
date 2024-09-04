<template>
    <h1>{{ domanda }}</h1>
</template>

<script>
export default {
    props: {
        domanda: {
            type: String,
            required: true
        }
    }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
