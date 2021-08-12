<template>
  <div>
    <h1>{{ timer }}</h1>
    <div class="board" :style="styles">
      <GameBox v-for="field in fields" :key="field.id" v-bind="field" @select="select" />
    </div>
  </div>
</template>

<script>
import GameBox from "../game-box/GameBox";
export default {
  name: 'GameBoard',
  components: { GameBox },
  props: {
    count: {
      type: Number,
      required: true
    }
  },
  data: () => ({
    selectedFirst: null,
    selectedSecond: null,
    fields: [],
    equals: 0,
    timer: null,
    interval: null
  }),
  computed: {
    styles(){
      return {
        gridTemplateColumns: `repeat(${this.$props.count}, 1fr)`,
        maxWidth: `${(this.$props.count * 110)}px`
      }
    },
  },
  methods: {
    select(field){
      if(!this.selectedFirst){
        this.open(field.id)
        this.selectedFirst = field;
      } else if(!this.selectedSecond){
        this.open(field.id)
        this.selectedSecond = field;
        this.compare();
      }
    },
    open(id){
      this.fields.find(field => field.id === id).show = true;
    },
    compare(){
      if(this.selectedFirst.value === this.selectedSecond.value){
        this.fields.forEach(field => {
          if(field.id === this.selectedFirst.id){
            field.selected = true
          }
          if(field.id === this.selectedSecond.id){
            field.selected = true
          }
        })
        this.equals ++;
        this.clear();
      } else {
        setTimeout(this.hide, 2000)
      }
    },
    hide(){
      this.fields.forEach(field => field.show = false);
      this.clear()
    },
    clear(){
      this.selectedFirst = null;
      this.selectedSecond = null;
    }
  },
  created() {
    const arr = [...Array.from({length: this.$props.count}, (_, i) => i + 1), ...Array.from({length: this.$props.count}, (_, i) => i + 1)];
    const sorted = arr.sort( () => 0.5 - Math.random());
    this.fields = sorted.map((num, i) => ({
      value: num,
      id: i,
      selected: false,
      show: false
    }))
    this.timer = this.$props.count * 10;
    this.interval = setInterval(() => {
      this.timer--;
      if(this.timer === 0){
        alert('Game Over, your score is ' + this.equals);
        clearInterval(this.interval);
      }
    }, 1000)
  },
  watch: {
    equals(val){
      if(val === this.$props.count){
        alert('Win')
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.board {
  display: grid;
  grid-gap: 10px;
  justify-content: center;
  margin: auto;
}
</style>