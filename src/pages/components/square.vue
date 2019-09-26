<template>
  <div class="beforeClick" :class="{afterClick:isClicked}" @click="handleClick"></div>
</template>

<script>
export default {
  name: 'square',
  props: {
    cannotChangeColor: Boolean,
    clearColor: Number
  },
  data () {
    return {
      isClicked: false
    }
  },
  methods: {
    handleClick () {
      if (this.cannotChangeColor === false && this.isClicked === false) {
        this.isClicked = true
        this.$emit('isClicked')
      }
    }
  },
  watch: {
    clearColor: function () {
      this.isClicked = false
    }
  }
}
</script>

<style scoped>
  .beforeClick{
    width: 50px;
    height: 50px;
    background-color: green;
  }
  .afterClick{
    width: 50px;
    height: 50px;
    background-color: red;
  }
</style>
