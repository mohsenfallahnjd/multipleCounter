<template>
  <div id="app">
    <div class="add-counter">
      <div class="add-counter__input">
        <!-- type="number" -->
        <b-form-input
          id="counter-input"
          v-model="stepValue"
          placeholder="Step"
          @keypress.enter="addCounter"
        />
        <label id="input-label" for="counter-input">
          This only accepts numbers like 1, 2, -5, 3.8, 3
        </label>
      </div>
      <b-button class="add-counter__btn" @click="addCounter">
        Add Counter
      </b-button>
    </div>
    <div class="counters-card">
      <Counter v-for="(counter, i) in counters" :key="i" :step="counter.step" />
    </div>
  </div>
</template>

<script>
import Counter from "@/components/Counter.vue";
export default {
  name: "App",
  components: { Counter },
  data: () => ({
    stepValue: "",
    counters: [
      {
        step: 1,
      },
      {
        step: 3,
      },
      {
        step: -2.6,
      },
    ],
  }),
  methods: {
    addCounter() {
      // check input != empty and the input`s Value != 0 and type of input = number \ else error
      if (
        this.stepValue != "" &&
        this.stepValue != 0 &&
        this.stepValue == parseFloat(this.stepValue)
      ) {
        //if input number = int, add new Counter
        if (parseFloat(this.stepValue) == Math.round(this.stepValue)) {
          this.pushCounter(this.stepValue);
        } else {
          //if input number = float with one decimal, add new Counter \ else error
          this.stepValue.split(".")[1].length > 1
            ? this.err()
            : this.pushCounter(this.stepValue);
        }
      } else {
        this.err();
      }
    },

    err() {
      // set the red border to Input and red color on Label if an error has happened
      document.getElementById("counter-input").style.borderColor = "#F20000";
      document.getElementById("counter-input").style.borderWidth = "1.3px";
      document.getElementById("input-label").style.color = "#F20000";
      setTimeout(() => {
        document.getElementById("counter-input").style.borderColor = "#000";
        document.getElementById("counter-input").style.borderWidth = "1px";
        document.getElementById("input-label").style.color = "#000";
        this.stepValue = "";
      }, 3000);
    },
    pushCounter(item) {
      // push NewObject of Counter to CountersList and Clean Input
      this.counters.push({
        step: parseFloat(item),
      });
      this.stepValue = "";
    },
  },
};
</script>

<style lang="sass">

#app
  overflow: hidden auto
  display: flex
  flex-direction: column
  align-items: center
  position: absolute
  top: 0
  left: 0
  right: 0
  bottom: 0
  padding: 1em
  .add-counter
    width: 80%
    padding: 1em
    margin: 1em
    display: flex
    background-color: #fafafa
    border: 1px solid #000
    border-radius: 0.25rem
    &__input
      flex-basis: 0
      flex-grow: 2
      input
        border-color: #000
        &::-webkit-inner-spin-button,&::-webkit-outer-spin-button
          -webkit-appearance: none
          margin: 0
        &:focus
          box-shadow: none
      label
        margin: .8em .3em 0
    &__btn
      flex-basis: 0
      flex-grow: 1
      margin-left: .8em
      height: calc(1.5em + 0.75rem + 2px)
      background-color: #000
      &:hover
        background-color: lighten(#000, 15%)
      &:focus
        box-shadow: none
  .counters-card
    width: 80%
    padding: 1em
    margin: 1em
    border-radius: 0.25rem
    background-color: #fafafa
    border: 1px solid #000
    position: relative
    display: flex
    flex-flow: row wrap
    justify-content: space-evenly
</style>
