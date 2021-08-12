<template>
  <div class="front-side">{{ $props.text }}</div>
</template>

<script>
export default {
  name: 'FrontSide',
  props: {
    text: {
      type: Number,
      required: true
    }
  }
}
</script>

<style lang="scss" scoped>
.front-side {
  width: 100%;
  height: 100%;
  border: 1px solid #000;
  background: darkgreen;
  display: flex;
  justify-content: center;
  align-items: center;
  color: #ffffff;
  font-size: 32px;
  font-family: Bahnschrift;
}
</style>