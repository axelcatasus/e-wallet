<template>
  <div class="form">
    <form 
    @submit.prevent="$emit('formcard-submit-emit', newCard)"
    @input="$emit('formcard-emit', newCard)"
    >
      <div class="num">
        <p>CARD NUMBER</p>
        <input
          class="number-input"
          type="text"
          inputmode="numeric"
          minlength="19"
          maxlength="19"
          @input="numberSpacer"
          v-model="newCard.cardNumber"
          onkeypress="return /[0-9]/i.test(event.key)"
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
          onkeypress="return /[a-ö, ' ']/i.test(event.key)"
          placeholder="FIRSTNAME LASTNAME"
          required
        >
      </div>
      <div class="expiry-ccv">
        <div class="expiry">
          <p>VALID THRU</p>
          <input 
            class="month-input"
            type="number"
            min="1"
            max="12"
            inputmode="numeric"
            @input="focusNext"
            v-model="newCard.expireMonth"
            maxlength="2"
            onkeypress="return /[0-9]/i.test(event.key)"
            list="months"
            placeholder="MM"
            required
          >
          <input
            class="year-input"
            type="number"
            min="22"
            max="30"
            inputmode="numeric"
            @input="focusNext"
            v-model="newCard.expireYear"
            minlength="2"
            maxlength="2"
            onkeypress="return /[0-9]/i.test(event.key)"
            list="years"
            placeholder="YY"
            required
          >
        </div>
        <div class="ccv">
          <p>CCV</p>
          <input
            class="ccv-input"
            type="number"
            inputmode="numeric"
            @input="focusNext"
            v-model="newCard.CCV"
            minlength="3"
            maxlength="3"
            onkeypress="return /[0-9]/i.test(event.key)"
            required
          >
        </div>
      </div>
      <div class="vendor">
        <p>VENDOR</p>
        <select 
          class="vendor-select"
          v-model="newCard.vendor"
          @input="focusNext"
          required
        >
          <option value="bitcoin">BITCOIN INC</option>
          <option value="blockchain">BLOCK CHAIN INC</option>
          <option value="evil">EVIL CORP</option>
          <option value="ninja">NINJA BANK</option>
        </select>
      </div>
      <div class="submit">
        <button class="add-card-button">ADD CARD</button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  props: {cards: Array},
  computed: {},
  methods: {
    created() {
      this.newCard.cardHolder = 'Firstname Lastname'
    },
    numberSpacer(event){
      this.focusNext(event)
      if(event.data != null){
        for(let number of this.spaceArray){
          if(number == this.newCard.cardNumber.length){
            this.newCard.cardNumber += ' '
          }
        }
      }
    },
    focusNext(event){
      for(let element of this.focusData){
        if(element.inputName === event.target.className){
          if(event.target.value.length === element.maxLength){
            document.querySelector(element.nextFocus).focus()
          }
        }
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
    months: ['01','02','03','04','05','06','07','08','09','10','11','12'],
    focusData: 
        [
          {
            inputName: 'number-input',
            maxLength: 19,
            nextFocus: '.name-input'
          },
          {
            inputName: 'month-input',
            maxLength: 2,
            nextFocus: '.year-input'
          },
          {
            inputName: 'year-input',
            maxLength: 2,
            nextFocus: '.ccv-input'
          },
          {
            inputName: 'ccv-input',
            maxLength: 3,
            nextFocus: '.vendor-select'
          },
          {
            inputName: 'vendor-select',
            maxLength: null,
            nextFocus: '.add-card-button'
          },
        ]
  }}
}
</script>

<style scoped>

input[type=number] {
-moz-appearance:textfield !important; /* Firefox */
}

input[type=number]::-webkit-inner-spin-button, 
input[type=number]::-webkit-outer-spin-button { 
  -webkit-appearance: none; 
  appearance: none;
  display: hidden;
  margin: 0;
  opacity: 1;
}

.form {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
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
  appearance: none !important;
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
  color: black;
}

input:focus {
  outline: none;
}

.expiry-ccv {
  display: grid;
  grid-template-areas: "expiry ccv";
  width: 22.1rem;
  justify-content: space-between;

}

.expiry input{
  width: 3rem;
  grid-area: "expiry";
  margin-right: .4rem;
  text-align: center;
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
  margin-top: 1.5rem;
  transition: all 200ms ease;
}

button:hover {
  background: rgba(0, 0, 0, 0.80);
  transition: all 400ms ease;
}

</style>