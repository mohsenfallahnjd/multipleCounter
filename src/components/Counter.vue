<template>
  <div class="counter">
    <div class="counter__header">step: {{ step }}</div>
    <div class="counter__body">
      <h1>{{ count | digits }}</h1>
      <b-button :disabled="disabledBtn" class="run-btn" @click="run">
        RUN
      </b-button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Counter",
  props: {
    step: {
      type: Number,
      required: true,
    },
  },
  data: () => ({
    count: 0,
    disabledBtn: false,
  }),
  methods: {
    run() {
      // disabled button and run add Step function
      this.disabledBtn = true;
      window.setInterval(() => {
        this.count += this.step;
      }, 1000);
    },
  },
  filters: {
    digits: (value) => {
      if (value == Math.trunc(value)) {
        return Math.trunc(value);
      } else {
        return value.toFixed(1); // return floatNumber with one decimal after add Step Value
      }
    },
  },
};
</script>

<style lang="sass" scoped>
.counter
    width: 180px
    height: 250px
    background-color: #fff
    border: 1px solid #000
    border-radius: 0.25rem
    margin: 1em
    &__header
        width: 100%
        height: 40px
        padding: .4em .8em
        border-bottom: 1px solid #000
    &__body
        width: 100%
        height: calc( 100% - 40px )
        padding: 1em
        display: flex
        flex-direction: column
        align-items: center
        justify-content: space-around
        h1
            font-size: 50px
            font-weight: 700
            overflow-wrap: anywhere
        .run-btn
            width: 69%
            background-color: #000
            &:hover
                background-color: lighten(#000, 15%)
            &:active
                background-color: #000 !important
                box-shadow: none !important
            &:focus
                box-shadow: none
</style>
