<template>
  <div class="add-card">
      <a @click="$emit('back')" class="back">&#60;</a>
      <h1 class="heading">ADD A NEW BANK CARD</h1>
    <p class="newcard">NEW CARD</p>
      <NewCardForm 
        @formcard-emit="cardPreview" 
        @formcard-submit-emit="submitCard"
        :cards="cards" 
      />
  </div>
</template>

<script>
import NewCardForm from "../components/NewCardForm.vue"

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

.add-card {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
}

.back {
  position: fixed;
  top: 1rem;
  left: 1.5rem;
  font-weight: bold;
  font-size: 2.5rem;
}

.back:hover {
  cursor: pointer;
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