<template>
  <div class="start-game">
    <h1>Please Write Even Number Which Will Render Your Number Square Fields</h1>
    <input type="number" v-model.trim.number="number" class="start-game__input" />
    <span class="start-game__input-error">{{ error }}</span>
    <button class="start-game__button" @click="start">Start</button>
  </div>
</template>

<script>
export default {
  name: 'StartGame',
  data: () => ({
    number: null,
    error: null
  }),
  methods: {
    start(){
      if(!this.number){
        return this.error = 'PLease Fill The Field';
      }
      if(this.number < 4){
        return this.error = 'The Number Should Be Greater Than 3';
      }
      if(this.number % 2 !== 0){
        return this.error = 'The Number Should Be Even';
      }
      this.$emit('start', this.number);
    }
  }
}
</script>

<style lang="scss" scoped>
.start-game {
  width: 65%;
  margin: auto;

  &__input {
    width: 300px;
    padding: 8px 5px;
    display: block;
    margin: 20px auto 5px;

    &::-webkit-outer-spin-button,
    &::-webkit-inner-spin-button {
      -webkit-appearance: none;
      -moz-appearance: textfield;
    }

    &-error {
      display: block;
      margin: 0 auto 10px;
      color: red;
      font-size: 12px;
      height: 15px;
    }
  }

  &__button {
    border: none;
    border-radius: 8px;
    padding: 12px 45px;
    background: #174e79;
    color: #ffffff;
  }
}
</style>