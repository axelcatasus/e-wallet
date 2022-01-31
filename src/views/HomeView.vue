<template>
  <div class="home">
    <h1>E-WALLET</h1>
    <div class="active-card" v-if="activeCard">
      <p>ACTIVE CARD</p>
      <Card :card="activeCard" :class="{'active-card-focus' : activeCardFocus}"/>
      <p class="remove-active" @click="showModal = true">REMOVE ACTIVE CARD</p>
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
      <Card v-for="card in filterActive" :key="card.cardNumber" @click="makeActive(card)" :card="card"/>
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
      this.activeCardFocus = true
      setTimeout(() => {this.activeCardFocus = false}, 400)
    },
    removeActive(){
      this.$emit('remove', this.activeCard)
      this.activeCard = this.cards[0]
      this.showModal = false
      this.activeCardFocus = true
      setTimeout(() => {this.activeCardFocus = false}, 400)
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
      activeCardFocus: false
    }}

}
</script>

<style scoped>

.home {
  display: flex;
  flex-direction: column;
  align-items: center;
}

h1 {
  margin-bottom: .5rem;
}

.remove-active {
  color: red;
  margin-top: 0.25rem;
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
  margin: 32vh auto;
  padding: 1rem;
  border: 1px solid #888;
  width: 12rem;
}

.remove-modal-content p {
  font-size: 1rem;
  font-weight: bold;
  color: red;
}

.remove-modal-content button {
  margin: .5rem;
  font-size: 1rem;
  width: 4rem;
  height: 3rem;
  font-family: 'PT Mono', monospace;
  border-radius: 4px;
  border: 1px black solid;
  color: black;
  background: white;
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
}

.active-card div {
  transition: all 400ms ease;
}

.active-card div:active {
  filter: brightness(1.2);
  transition: all 400ms ease;
  transform: scale(1.05)
}

.add-button {
  position: sticky;
  justify-self: flex-end;
  bottom: 1rem;
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
  background: rgba(240, 240, 240);
  transition: all 400ms ease;
}

.card-stack {
  display: grid;
  margin-top: 1rem;
  grid-auto-rows: 2.5rem;
  margin-bottom: 14rem;
}

.active-card-focus {
  animation: activated ease 400ms;
}
@keyframes activated {
  0% {
    filter: brightness(1);
    transform: scale(1)
  }
  50% {
    filter: brightness(1.2);
    transform: scale(1.02)
  }
  100% {
    filter: brightness(1);
    transform: scale(1)
  }
}


</style>