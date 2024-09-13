  <script>
  import Domande from './components/Domande.vue';
  import Risposte from './components/Risposte.vue';
  import { domande } from './domande.js'; // file esterno per mantenere il codice pulito

  export default {
    components: {
      Domande,
      Risposte
    },

    data() {
      return {
        domande,
        option1: "Hai completato tutte le domande! Ricarica la pagina per riprovare.",
        option2: "Il gioco è terminato. Ricarica la pagina per riprovare.",
        domandaCorrente: null
      };
    },

    mounted() { // al caricamento della pagina seleziona una domanda random
      this.selezionaDomandaRandom();
    },

    methods: {
      test() {
        console.log('ciao');
      },

      selezionaDomandaRandom() {
        // Se non ci sono più domande, il gioco termina
        if (this.domande.length === 0) {
          this.domandaCorrente = null;
          return;
        }

        const indiceRandom = Math.floor(Math.random() * this.domande.length);
        this.domandaCorrente = this.domande[indiceRandom];

        // Rimuoviamo la domanda selezionata dall'array delle domande
        // in modo che non si ripeta
        this.domande.splice(indiceRandom, 1);
      },

      controllaRisposta(risposta) {
        if (risposta === this.domandaCorrente.rispostaCorretta) {
          alert('Risposta Corretta!');
          setTimeout(() => {
            this.selezionaDomandaRandom();
          }, 1500);
        } else {
          alert("Risposta sbagliata! Hai perso!");
          // Il gioco termina in caso di risposta sbagliata
          this.domandaCorrente = null;
        }
      }
    }
  };
</script>

  
<template>

  <Domande v-if="domandaCorrente" :domanda="domandaCorrente.domanda" />
  <Risposte v-if="domandaCorrente" :risposte="domandaCorrente.risposte" @selezionaRisposta="controllaRisposta" />

  <!-- Messaggio di fine gioco o schermata iniziale -->
  <p v-else>{{ domande.length === 0 ? option1 : option2 }}</p>

</template>


<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
}
</style>
