<template>
  <div class="card" :class="classGenerator" @click="$emit('click')">
    <div class="wifichip">
      <img class="wifi" v-if="this.card.vendor == '' || this.card.vendor == 'bitcoin'" src="../assets/wifi.svg">
      <img class="wifi-white" v-else src="../assets/wifi_white.svg">
      <div class="chipcontainer">
        <img class="chip" src="../assets/chip.svg">
      </div>
    </div>
    <img v-if="this.card.vendor" v-bind:src="this.imgSrc" class="vendor-img">
    <p class="card-number">{{number}}</p>
    <!-- <p class="card-number">{{card.cardNumber}}</p> -->
    <div class="card-holder">
      <p class="card-holder-title">CARDHOLDER NAME</p>
      <!-- <p v-if="this.card.cardHolder" class="card-holder-name">{{card.cardHolder.toUpperCase()}}</p> -->
      <p class="card-holder-name">{{name}}</p>
    </div>
    <div class="valid-date">
      <p>VALID THRU</p>
      <!-- <p class="exp-date">{{card.expireMonth}}/{{card.expireYear}}</p> -->
      <p class="exp-date">{{month}}/{{year}}</p>
    </div>
  </div>
</template>
<script>
export default {
  props: {card: Object},
  data(){return{
    x: 'X'
  }},
  computed: {
    imgSrc() {
      return require("../assets/" + (this.card.vendor) + ".svg")
    },
    classGenerator(){
      return this.card.vendor
    },
    number() {
      if(this.card.cardNumber == ''){
        return 'XXXX XXXX XXXX XXXX'
      } else {
        return this.card.cardNumber.replace(/\d{4}(?=.)/g, '$& ');
      }
    },
    name() {
      if(this.card.cardHolder == ''){
        return 'FIRSTNAME LASTNAME'
      } else {
        return this.card.cardHolder.toUpperCase()
      }
    },
    month() {
      if(this.card.expireMonth == ''){
        return 'MM'
      } else {
        return this.card.expireMonth
      }
    },
    year() {
      if(this.card.expireMonth == ''){
        return 'YY'
      } else {
        return this.card.expireYear
      }
    },
  }
}
</script>


<style scoped>

p {
  color: black;
  
}

.card {
  max-width: 21rem;
  width: 90vw;
  max-height: calc(21rem * 0.618); 
  height: calc(90vw * 0.618);
  display: grid;
  /* max-width: 17.5rem; */
  /* max-height: 10rem; */
  /* width: 21rem; */
  /* height: 12rem; */
  /* aspect-ratio: 3.5/2; */
  border-radius: 8px;
  background: linear-gradient(248.3deg, rgba(255, 255, 255, 0.24) 0%, rgba(255, 255, 255, 0) 100%), #D0D0D0;
  text-shadow: 1px 0px 0px rgba(0, 0, 0, 0.15), 0px 1px 0px rgba(0, 0, 0, 0.05), -1px 0px 0px rgba(0, 0, 0, 0.05), 0px -1px 0px rgba(0, 0, 0, 0.15);
  grid-template-areas: 
  "wifichip . . vendor-img"
  "card-number card-number card-number card-number "
  "card-holder . . valid-date";
  padding: 1rem;
  box-shadow: rgba(7, 7, 7, 0.2) 0px 2px 15px;
  transition: filter 200ms ease;
  
}

/* .card:hover {
  filter: brightness(1.1);
  transition: filter 200ms ease;
} */

.vendor-img {
  grid-area: vendor-img;
  align-self: flex-start;
  justify-self: flex-end;
  height: 5rem;
}

.card-number{
  grid-area: card-number;
  font-size: 1.8rem;
  text-align: center;
  margin: 0;
  align-self: center;
}

.card-holder{
  grid-area: card-holder;
  align-self: flex-end;
}

.card-holder-name, .exp-date{
  font-size: 1.2rem;
  margin: 0 0 2rem 0;
  line-height: 0;
}

.valid-date{
  grid-area: valid-date;
  text-align: right;
  align-self: flex-end;
}

.wifichip {
  display: flex;
  flex-direction: column;
  align-items: center;
  grid-area: wifichip;
  align-self: flex-start;
  justify-self: flex-start;
}

.wifi, .chip, .wifi-white {
  height: 2rem;
}

.chip {
  width: fit-content;
}

.wifi {
  opacity: 0.5;
}

.chipcontainer {
  display: flex;
  width: 2.7rem;
  border: solid .01rem #8d8a86;
  background: linear-gradient(248.04deg, #d8d3cd 0%, #8d8a86 99%);
  border-radius: 8px;
  box-shadow: rgba(149, 157, 165, 0.2) 0px 8px 24px;
}

.bitcoin {
  background: linear-gradient(248.04deg, rgba(255, 255, 255, 0.15) 0%, rgba(255, 255, 255, 0) 99.07%), #FFAE34;
}

.blockchain {
  background: linear-gradient(248.52deg, rgba(0, 0, 0, 0.15) 1.49%, rgba(0, 0, 0, 0) 100%), #8B58F9;
}
.blockchain p {
  color: rgb(230, 230, 230);
}

.evil {
  background: linear-gradient(248.3deg, rgba(0, 0, 0, 0.16) 0%, rgba(0, 0, 0, 0) 100%), #F33355;
}
.evil p {
  color: rgb(211, 211, 211);
  
}
.ninja {
  background: linear-gradient(248.3deg, rgba(255, 255, 255, 0.15) 0%, rgba(255, 255, 255, 0) 100%), #222222;
}

.ninja p {
  color: rgb(211, 211, 211);
}


</style>