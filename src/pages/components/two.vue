<template>
  <div class="wrapper">
    <square v-for="(item,index) of list" :key="index" @isClicked="addCount" :cannotChangeColor="cannotClick" :clearColor="clearColor"></square>
  </div>
</template>

<script>
import square from './square'
export default {
  name: 'two',
  props: {
    cannotClick: Boolean,
    clear: Number
  },
  components: {
    square
  },
  data () {
    return {
      list: [true, true, true, true, true],
      count: 0,
      canClick: true,
      clearColor: 0
    }
  },
  methods: {
    addCount () {
      if (this.cannotClick === true) {
        this.canClick = false
      } else {
        this.canClick = true
      }
      if (this.canClick) {
        this.count++
        this.$emit('forbiddenClick') // 向外触发一个禁止点击其它行的事件
        if (this.count === 5) {
          this.$emit('twoAllClicked')
        }
      }
    }
  },
  watch: {
    clear: function () {
      this.count = 0
      this.clearColor++
    }
  }
}
</script>

<style scoped>
  .wrapper{
    display: flex;
    justify-content: space-around;
    margin-top: 10px;
  }
</style>
