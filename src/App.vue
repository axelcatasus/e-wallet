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
  methods: {
    pushNewCard(newCard){
      this.cards.push(newCard)
      this.view = "HomeView"
    },
    removeCard(removeCard){
      for(let i = 0; i < this.cards.length; i++){
        if(removeCard == this.cards[i]) {
          this.cards.splice(i, 1)
        }
      }
    }
    },

  data(){return{
    view: "HomeView",
    cards: []
  }}
}
</script>


<style>
@import url('https://fonts.googleapis.com/css2?family=PT+Mono&family=Source+Sans+Pro:wght@400;700&display=swap');


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