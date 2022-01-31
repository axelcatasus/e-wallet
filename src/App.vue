<template>
  <div id="app">
    <DarkMode class="darkmode"/>
    <HomeView v-if="view=='HomeView'" :cards="cards" @change-view="view='AddCardView'" @remove="removeCard" />
    <AddCardView v-if="view=='AddCardView'" :cards="cards" @addcard-emit="pushNewCard" @back="view='HomeView'" />
  </div>
</template>

<script>
import HomeView from "./views/HomeView.vue";
import AddCardView from "./views/AddCardView.vue";
import DarkMode from "./components/DarkMode.vue"

export default {
  // components: {HomeView, AddCardView},
  components: {HomeView, AddCardView, DarkMode},
  beforeMount() {
    if(localStorage.cards){
    this.cards = JSON.parse(localStorage.getItem('cards'))
    }
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
    cards: [
      {
      vendor: "bitcoin", 
      cardNumber: "1234567812345678", 
      cardHolder: "AXEL CATASÚS", 
      expireMonth: "03", 
      expireYear: "30", 
      CCV: '666'
      },
      {
      vendor: "evil", 
      cardNumber: "9876543210123456", 
      cardHolder: "LAVID DUNDHOLM", 
      expireMonth: "05", 
      expireYear: "23", 
      CCV: '666'
      },
      {
      vendor: "blockchain", 
      cardNumber: "8008580085800500", 
      cardHolder: "VIKARD RIRTA", 
      expireMonth: "07", 
      expireYear: "23", 
      CCV: '666'
      },
      ]
  }}
}
</script>


<style>
@import url('https://fonts.googleapis.com/css2?family=PT+Mono&family=Source+Sans+Pro:wght@400;700&display=swap');

html {
  overflow: hidden;
}

.darkmode {
  position: fixed;
  display: sticky;
  transform: rotate(90deg);
  margin: 1.5rem auto;
  right: 1rem;
}

h1 {
  font-family: 'Source Sans Pro', sans-serif;
}

p {
  font-family: 'PT Mono', monospace;
}
</style>