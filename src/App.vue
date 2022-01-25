<template>
  <div id="app">
    <HomeView v-if="view=='HomeView'" :cards="cards" @change-view="view='AddCard'" @remove="removeCard" />
    <AddCardView v-if="view=='AddCard'" :cards="cards" @addcard-emit="pushNewCard" />
  </div>
</template>

<script>
import HomeView from "./views/HomeView.vue";
import AddCardView from "./views/AddCardView.vue";

export default {
  components: {HomeView, AddCardView},
  beforeMount() {
    this.cards = JSON.parse(localStorage.getItem('cards'))
  },
  methods: {
    pushNewCard(newCard){
      this.cards.push(newCard)
      this.view = "HomeView"
      localStorage.setItem('cards', JSON.stringify(this.cards))
    },
    removeCard(removeCard){
      for(let i = 0; i < this.cards.length; i++){
        if(removeCard === this.cards[i]) {
          this.cards.splice(i, 1)
          localStorage.setItem('cards', JSON.stringify(this.cards))
        }
      }
    }
    },

  data(){return{
    view: "HomeView",
    cards: [{
      vendor: "bitcoin", 
      cardNumber: "1234 5678 1234 5678", 
      cardHolder: "AXEL CATASÚS", 
      expireMonth: "3", 
      expireYear: "60", 
      CCV: '666'
      },
      {
      vendor: "blockchain", 
      cardNumber: "0000 0000 0000 0000", 
      cardHolder: "RIKARD VIRTA", 
      expireMonth: "3", 
      expireYear: "23", 
      CCV: '666'
      },
      {
      vendor: "evil", 
      cardNumber: "1337 1337 1337 1337", 
      cardHolder: "OSCAR ARRHENIUS", 
      expireMonth: "13", 
      expireYear: "37", 
      CCV: '666'
      },
      {
      vendor: "ninja", 
      cardNumber: "1338 1337 1337 1337", 
      cardHolder: "IDAN CHEAPROOT", 
      expireMonth: "13", 
      expireYear: "37", 
      CCV: '666'
      }]
  }}
}
</script>


<style>
@import url('https://fonts.googleapis.com/css2?family=PT+Mono&family=Source+Sans+Pro:wght@400;700&display=swap');

html {
  overflow: hidden;
}

#app{
  padding: 0rem;
}

h1 {
  font-family: 'Source Sans Pro', sans-serif;
}

p {
  font-family: 'PT Mono', monospace;
}
</style>