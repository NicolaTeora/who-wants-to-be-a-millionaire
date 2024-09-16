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
        msgEnd: "Risposta sbagliata! Hai perso, ricarica la pagina per riprovare",
        domandaCorrente: null,
        giocoIniziato: false, //Gestione schermata iniziale
        giocoInCorso: false  // Variabile per visualizzare il contenuto del gioco dopo la transizione
      };
    },

    mounted() {
      // al caricamento della pagina seleziona una domanda random
      this.selezionaDomandaRandom();
    },

    methods: {
      iniziaGioco() {
        this.giocoIniziato = true;
        // Avvia il gioco selezionando la prima domanda
        this.selezionaDomandaRandom();
      },

      // Questo metodo sarà chiamato dopo che la schermata iniziale è completamente scomparsa
      avviaDomande() {
        this.giocoInCorso = true;
        this.selezionaDomandaRandom();
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
          // alert('Risposta Corretta!');
          setTimeout(() => {
            this.selezionaDomandaRandom();
          }, 1500);
        } else {
          // Il gioco termina in caso di risposta sbagliata
          setTimeout(() => {
            this.domandaCorrente = null;
          }, 1500);

          this.option2 = this.msgEnd;
        }
      }
    }
  };
</script>

  
<template>
  <transition name="fade" @after-leave="avviaDomande()">

    <div v-if="!giocoIniziato" class="start-screen">
      <h1>Chi Vuol Essere Milionario</h1>
      <button @click="iniziaGioco">Start Game</button>
    </div>

    <div v-else>

      <Domande v-if="domandaCorrente" :domanda="domandaCorrente.domanda" />
      <Risposte v-if="domandaCorrente" :risposte="domandaCorrente.risposte"
        :rispostaCorretta="domandaCorrente.rispostaCorretta" @selezionaRisposta="controllaRisposta" />

      <!-- Messaggio di fine gioco o schermata iniziale -->
      <p v-else>{{ domande.length === 0 ? option1 : option2 }}</p>
    </div v-else>
  </transition>

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

.start-screen button {
  padding: 10px 20px;
  font-size: 1.5rem;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;

  &:hover {
    background-color: #45a049;
  }
}

/* Transizione per la dissolvenza */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>
