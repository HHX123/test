<template>
  <div>
    <headerTop :flag="flag" @afterSubmit = "afterSubmit" @restart="restart"></headerTop>
    <one @oneAllClicked = "isAllClicked" :cannotClick="oneCannotClick" @forbiddenClick = "forbiddenClick23" :clear="clearAll"></one>
    <two @twoAllClicked = "isAllClicked();changeData()" :cannotClick="twoCannotClick" @forbiddenClick = "forbiddenClick13" :clear="clearAll"></two>
    <three @threeAllClicked = "isAllClicked" :cannotClick="threeCannotClick" @forbiddenClick = "forbiddenClick12" :clear="clearAll"></three>
  </div>
</template>

<script>
import one from './components/one'
import two from './components/two'
import three from './components/three'
import headerTop from './components/headerTop'
export default {
  name: 'index',
  components: {
    one,
    two,
    three,
    headerTop
  },
  data () {
    return {
      allClicked: 0,
      flag: false,
      oneCannotClick: false,
      twoCannotClick: false,
      threeCannotClick: false,
      twoRowAllClick: false, // 当第二行点完后一三行可以随意点击
      clearAll: 0
    }
  },
  methods: {
    isAllClicked () {
      this.allClicked++
      if (this.allClicked === 3) {
        this.flag = true
      }
    },
    changeData () { // 第二行全部点击完后执行的函数
      this.twoRowAllClick = true
    },
    forbiddenClick23 () {
      this.twoCannotClick = true
      this.threeCannotClick = true
    },
    forbiddenClick13 () {
      this.oneCannotClick = true
      this.threeCannotClick = true
    },
    forbiddenClick12 () {
      this.oneCannotClick = true
      this.twoCannotClick = true
    },
    afterSubmit () {
      // 第二行没有全部被点击时点击完第一行
      let firstRowAfterClicked = this.oneCannotClick === false && this.twoCannotClick === true && this.threeCannotClick === true && this.twoRowAllClick === false
      if (firstRowAfterClicked) {
        this.oneCannotClick = false
        this.twoCannotClick = false
        this.threeCannotClick = true
      }
      // 第二行全部被点击时点击完第一行
      let firstRowAfterClicked2 = this.oneCannotClick === false && this.twoCannotClick === true && this.threeCannotClick === true && this.twoRowAllClick === true
      if (firstRowAfterClicked2) {
        this.oneCannotClick = false
        this.twoCannotClick = true
        this.threeCannotClick = false
      }

      // 第二行没有全部被点击时点击完第三行
      let thirdRowAfterClicked = this.threeCannotClick === false && this.twoCannotClick === true && this.oneCannotClick === true && this.twoRowAllClick === false
      if (thirdRowAfterClicked) {
        this.oneCannotClick = true
        this.twoCannotClick = false
        this.threeCannotClick = false
      }

      // 第二行全部被点击时点击完第三行
      let thirdRowAfterClicked2 = this.threeCannotClick === false && this.twoCannotClick === true && this.oneCannotClick === true && this.twoRowAllClick === true
      if (thirdRowAfterClicked2) {
        this.oneCannotClick = false
        this.twoCannotClick = true
        this.threeCannotClick = false
      }

      // 点击完第二行后所有行都能被点击
      let secRowAfterClicked = this.twoCannotClick === false && this.oneCannotClick === true && this.threeCannotClick === true
      if (secRowAfterClicked) {
        this.oneCannotClick = false
        this.twoCannotClick = false
        this.threeCannotClick = false
      }
      // console.log(this.twoRowAllClick,'-------',this.oneCannotClick,this.twoCannotClick,this.threeCannotClick)
    },

    // 重新开始
    restart () {
      this.oneCannotClick = false
      this.twoCannotClick = false
      this.threeCannotClick = false
      this.twoRowAllClick = false
      this.allClicked = 0
      this.flag = false
      this.clearAll++
    }
  }
}
</script>

<style scoped>

</style>
