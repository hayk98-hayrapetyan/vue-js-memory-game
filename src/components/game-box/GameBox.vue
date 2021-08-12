<template>
  <div @click="select" class="box">
    <transition name="rotate" mode="out-in">
      <component :is="current" :text="$props.value"></component>
    </transition>
  </div>
</template>

<script>
import BackSide from "../back-side/BackSide";
import FrontSide from "../front-side/FrontSide";

export default {
  name: 'GameBox',
  components: {
    BackSide,
    FrontSide
  },
  props: {
    value: {
      type: Number,
      required: true
    },
    id: {
      type: Number,
      required: true
    },
    selected: {
      type: Boolean,
      required: true
    },
    show: {
      type: Boolean,
      default: false
    }
  },
  data: () => ({
    current: BackSide
  }),
  methods: {
    select(){
      if(!this.$props.selected) {
        this.$emit('select', {id: this.$props.id, value: this.$props.value});
      }
    }
  },
  watch: {
    show(val){
      if(!this.$props.selected) {
        this.current = val ? 'FrontSide' : 'BackSide';
      }
    },
    selected(val){
      if(val){
        this.current = 'FrontSide';
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.box {
  width: 100px;
  height: 100px;
}

.rotate-enter {
  transform: perspective(500px) rotate3d(0, 1, 0, 90deg);
}
.rotate-enter-active,
.rotate-leave-active {
  transition: 0.5s;
}
.rotate-leave-to {
  transform: perspective(500px) rotate3d(0, 1, 0, -90deg);
}

</style>