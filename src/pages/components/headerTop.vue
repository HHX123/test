<template>
  <div class="wrapper">
    <button @click="changePerson();changeCanClick()" v-show="showBtn">确认</button>
    <p v-show="isShowA">A胜利</p>
    <p v-show="isShowB">B胜利</p>
    <button @click="restart">重新开始</button>
  </div>
</template>

<script>
export default {
  name: 'headerTop',
  props: {
    flag: Boolean
  },
  data () {
    return {
      person: 'B',
      isShowA: false,
      isShowB: false,
      showBtn: true
    }
  },
  methods: {
    changePerson () {
      this.person === 'A' ? (this.person = 'B') : (this.person = 'A')
      if (this.flag) {
        this.showBtn = false
        if (this.person === 'A') {
          this.isShowB = true
        } else {
          this.isShowA = true
        }
      }
    },
    changeCanClick () {
      this.$emit('afterSubmit')
    },
    restart () {
      this.person = 'B'
      this.isShowA = false
      this.isShowB = false
      this.showBtn = true
      this.$emit('restart')
    }
  }
}
</script>

<style scoped>
.wrapper {
  display: flex;
  align-items: center;
  height: 25px;
}
</style>
