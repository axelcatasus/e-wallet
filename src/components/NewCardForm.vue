<template>
  <div class="form">
    <Card :card="newCard" />
    <form 
      @submit.prevent="submitCard"
      @input="inputHandler"
    >
      <div class="num">
        <p>CARD NUMBER</p>
        <input
          class="number-input"
          :class="{ numerror : errorMessage != ''}"
          ref="number"
          type="text"
          inputmode="numeric"
          minlength="16"
          maxlength="16"
          v-model="newCard.cardNumber"
          @active="errorHandler"
          onkeypress="return /[0-9, Enter]/i.test(event.key)"
          placeholder=""
          required 
        >
      </div>
      <div class="name-section">
        <p>CARDHOLDER NAME</p>
        <input
          class="name-input"
          type="text"
          maxlength="20"
          v-model="newCard.cardHolder"
          onkeypress="return /[a-ö, ' ', Enter]/i.test(event.key)"
          placeholder="FIRSTNAME LASTNAME"
          required
        >
      </div>
      <div class="expiry-ccv">
        <div class="expiry">
          <p>VALID THRU</p>
          <select 
            :class=" { opaque: monthOpaque }"
            @focus="monthOpaque = false"
            v-model="newCard.expireMonth"
            required
          >
            <option value="" disabled hidden>MM</option>
            <option v-for="month in this.months" :key="month" :value="month">{{month}}</option>
          </select>
          <select 
            :class="{ opaque: yearOpaque }"
            @focus="yearOpaque = false"
            v-model="newCard.expireYear"
            required
          >
            <option value="" disabled hidden>YY</option>
            <option v-for="year in 10" :key="year" :value="year+21">{{21+year}}</option>
          </select>
        </div>
        <div class="ccv">
          <p>CCV</p>
          <input
            class="ccv-input"
            type="text"
            inputmode="numeric"
            v-model="newCard.CCV"
            minvalue="0"
            minlength="3"
            maxlength="3"
            onkeypress="return /[0-9, Enter]/i.test(event.key)"
            required
          >
        </div>
      </div>
      <div class="vendor">
        <p>VENDOR</p>
        <select 
          class="vendor-select"
          v-model="newCard.vendor"
          required
        >
          <option value="bitcoin">BITCOIN INC</option>
          <option value="blockchain">BLOCK CHAIN INC</option>
          <option value="evil">EVIL CORP</option>
          <option value="ninja">NINJA BANK</option>
        </select>
      </div>
        <p class="error">{{errorMessage}}</p>
      <div class="submit">
        <button class="add-card-button" ref="addCardButton">ADD CARD</button>
      </div>
    </form>
  </div>
</template>

<script>
import Card from "../components/Card.vue"

export default {
  components: {Card},
  props: {cards: Array},
  computed: {},
  methods: {
    inputHandler(){
      this.$emit('formcard-emit', this.newCard)
    },
    errorHandler(){
      if(this.errorMessage != ''){
        this.errorMessage = ''
      }
    },
    submitCard(){
      if (this.cards.find((number) => number.cardNumber == this.newCard.cardNumber)){
        this.errorMessage = `CARD ${this.newCard.cardNumber} ALREADY ADDED`
      } else {
        this.errorMessage = ""
        this.$emit('formcard-submit-emit', {...this.newCard})
      }
    },
  },
  data(){return{
    newCard:
        {
          vendor: "", 
          cardNumber: "", 
          cardHolder: "", 
          expireMonth: "", 
          expireYear: "", 
          CCV: ''
        },
    spaceArray: [4, 9, 14],
    errorMessage: '',
    months: ['01','02','03','04','05','06','07','08','09','10','11','12'],
    monthOpaque: true,
    yearOpaque: true,
  }}
}
</script>

<style scoped>

.form {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.error {
  position: fixed;
  color: red;
  font-size: 1rem;
  margin-top: -1rem;
  font-family: 'Source Sans Pro', sans-serif;
  text-align: center;
  justify-self: center;
}

.numerror {
  border: 2px red solid;
}

form {
  /* width: 24rem; */
  width: 100%;
  display: grid;
  justify-content: center;
  margin-top: 2rem;
}

p {
  margin-bottom: .1rem;
  margin-left: .1rem;
  font-size: .75rem;
  color: rgba(0, 0, 0, .8)
}

input {
  height: 2rem;
  border: 1px black solid;
  width: 21rem;
  padding: 0.5rem;
  font-size: 1rem;
  border-radius: 8px;
  font-family: 'PT Mono', monospace;
  color: black;
  text-transform: uppercase;
}

input::placeholder {
  color: black
}

.expiry-ccv {
  display: grid;
  grid-template-areas: "expiry ccv";
  /* width: 22.1rem; */
  justify-content: space-between;

}

.expiry select{
  width: 4rem;
  background: white url('../assets/arrow.svg') no-repeat center right .5rem;
  grid-area: "expiry";
  margin-right: .4rem;
  text-align: left;
  background-size: 10px;
  border: 1px black solid;
  padding: .5rem;
  font-size: 1rem;
  border-radius: 8px;
  font-family: 'PT Mono', monospace;
  color: black;
}

.opaque {
  color: #777777 !important;
}

.ccv input {
  grid-area: "ccv";
  width: 8.5rem;
}


.vendor select{
  width: 100%;
}

select {
  height: 2rem;
  border-radius: 8px;
  height: 3rem;
  margin: 0;
  background: white url('../assets/arrow.svg') no-repeat center right 1rem;
  background-size: 10px;
  appearance: none;
  border: 1px black solid;
  width: 21.1rem;
  padding: .5rem;
  font-size: 1rem;
  border-radius: 8px;
  font-family: 'PT Mono', monospace;
  color: black;
  text-transform: uppercase;
}

select, option {
  font-size: 1rem;
}

button {
  width: 100%;
  height: 3.5rem;
  font-size: 1.2rem;
  font-family: 'PT Mono', monospace;
  border-radius: 8px;
  border: 1px black solid;
  color: white;
  background: black;
  margin-top: 2.5rem;
  transition: all 200ms ease;
}

button:hover {
  background: rgba(0, 0, 0, 0.80);
  transition: all 400ms ease;
}

</style>