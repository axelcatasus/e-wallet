<template>
  <div class="home">
    <h1>E-WALLET</h1>
    <div class="active-card" v-if="activeCard">
      <p>ACTIVE CARD</p>
      <Card :card="activeCard"/>
      <p class="remove-active" @click="showModal = true">REMOVE CARD</p>
      <div v-if="showModal" class="remove-modal-mask" @click.self="showModal = false">
        <div class="remove-modal-content">
          <p>REMOVE CARD?</p>
          <div>
            <button @click="removeActive">YES</button>
            <button @click="showModal = false">NO</button>
          </div>
        </div>
      </div>
    </div>
      <p class="card-stack-label" v-if="this.cards.length > 1">YOUR CARDS</p>
    <div class="card-stack">
      <Card v-for="card in filterActive" :key="card.cardNumber" @click="()=>makeActive(card)" :card="card"/>
    </div>
      <button class="add-button" @click="$emit('change-view')">ADD A NEW CARD</button>
  </div>
</template>

<script>
import Card from "../components/Card.vue"

export default {
  props:{cards: Array},
  components: {Card},
  methods:{
    makeActive(card){
      this.activeCard = card
    },
    removeActive(){
      this.$emit('remove', this.activeCard)
      this.activeCard = this.cards[0]
      this.showModal = false
    }
  },
  computed:{
    filterActive(){
      return this.cards.filter(card => card != this.activeCard)
    },
  },
    data(){return{
      activeCard: this.cards[0],
      showModal: false,
    }}

}
</script>

<style scoped>

.home {
  display: flex;
  flex-direction: column;
  /* justify-content: center; */
  align-items: center;
}

h1 {
  margin-bottom: .5rem;
}

.remove-active {
  /* position: fixed; */
  /* font-size: 2rem; */
  color: red;
  margin: 0;
  /* right: 15rem; */
}

.remove-modal-mask{
  position: fixed;
  z-index: 1;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0,0,0,0.4);
}

.remove-modal-content {
  display: flex;
  z-index: 0;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background-color: #fefefe;
  border-radius: 8px;
  margin: 35% auto;
  padding: 1rem;
  border: 1px solid #888;
  width: 40%;
}

.remove-modal-content p {
  font-size: 1rem;
  font-weight: bold;
  color: red;
}

.remove-modal-content button {
  margin: .5rem;
  width: 4rem;
  height: 3rem;
  font-family: 'PT Mono', monospace;
  border-radius: 4px;
  border: 1px black solid;
  color: black;
  background: white;
}

.remove-modal-content button:hover {
  background: #EEEEEE;
  font-weight: bold;
}


.remove-active:hover {
  cursor: pointer;
}

p {
  margin-bottom: .3rem;
  font-family: 'Source Sans Pro', sans-serif;
  color: rgba(34, 34, 34, 0.6);
  font-size: .7rem;
}

.card-stack-label {
  margin: -.65rem;
}

.active-card {
  margin-bottom: 2rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  transition: all 200ms ease;
}

.add-button {
  position: sticky;
  justify-self: flex-end;
  /* bottom: 1rem; */
  /* margin-top: 14rem; */
  width: 22.5rem;
  height: 3.5rem;
  font-size: 1.2rem;
  font-family: 'PT Mono', monospace;
  border-radius: 8px;
  border: 1px black solid;
  color: black;
  background: white;
  transition: all 200ms ease;
}

.add-button:hover {
  background: rgba(240, 240, 240, 0.8);
  transition: all 400ms ease;
}

.card-stack {
  display: grid;
  margin-top: 1rem;
  grid-auto-rows: 2.5rem;
  margin-bottom: 13rem;
}

/* .card-stack div {
  position: relative;
  overflow-x: visible;
}

.card-stack {
  max-height: 20rem;
  padding-top: 1rem;
  bottom: 6rem;
  width: 100%;
}

.card-stack > div:hover {
  transform: translateY(-.25rem);
  transition: all 200ms ease;
}

.card-stack > div{
  transition: all 200ms ease;
  margin: 0 auto;
}

.card-stack div:nth-of-type(1){
  position: static;
}

.card-stack div:nth-of-type(2){
  position: relative;
  top: -12.5rem;
}

.card-stack div:nth-of-type(3){
  position: relative;
  top: -25rem;
}

.card-stack div:nth-of-type(4){
  position: relative;
  top: -37.5rem;
}

.card-stack div:nth-of-type(5){
  position: relative;
  top: -50rem;
}

.card-stack div:nth-of-type(6){
  position: relative;
  top: -62.5rem;
}

.card-stack div:nth-of-type(7){
  position: relative;
  top: -78rem;
}
.card-stack div:nth-of-type(8){
  position: relative;
  top: -90.5rem;
}
.card-stack div:nth-of-type(9){
  position: relative;
  top: -103rem;
}
.card-stack div:nth-of-type(10){
  position: relative;
  top: -115.5rem;
}
.card-stack div:nth-of-type(11){
  position: relative;
  top: -128rem;
}
.card-stack div:nth-of-type(12){
  position: relative;
  top: -140.5rem;
} */




</style>