<template>
  <div class="add-card">
    <h1>ADD A NEW BANK CARD</h1>
    <p class="newcard">NEW CARD</p>
      <!-- <Card v-if="templateCheck" :card="templateCard" class="card"/>
      <Card v-else :card="card" class="card"/> -->
      <NewCardForm 
        @formcard-emit="cardPreview" 
        @formcard-submit-emit="submitCard"
        :cards="cards" 
      />
  </div>
</template>

<script>
import NewCardForm from "../components/NewCardForm.vue"
// import Card from "../components/Card.vue"

export default {
  props:{cards: Array},
  computed: {
    templateCheck(){
      if(Object.keys(this.card).length == 0){
        return true
      } else {
        return false
      }
      }},
  data(){return{
    card: {},
    templateCard:
      {
        vendor: "", 
        cardNumber: "XXXX XXXX XXXX XXXX", 
        cardHolder: "firstname lastname", 
        expireMonth: "13", 
        expireYear: "37", 
        CCV: ''
      },
  }},
  components: {NewCardForm},
  // components: {NewCardForm, Card},
  methods: {
    cardPreview(formCard){
      this.card = formCard
    },
    submitCard(newCard){
      this.$emit('addcard-emit', newCard)
    },
  }
}
</script>

<style>
.add-card{
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
}

.card {
  width: 100%;
}

.newcard {
  text-align: center;
  margin: 0;
  margin-bottom: .3rem;
  font-family: 'Source Sans Pro', sans-serif;
  color: rgba(34, 34, 34, 0.6);
  font-size: .7rem;
}
</style>