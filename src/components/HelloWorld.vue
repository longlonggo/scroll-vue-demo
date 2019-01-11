<template>
  <div class="hello">
    <scroll :list="list" @load="onLoad" ref='pullBox' />
  </div>
</template>

<script>
  import scroll from './scroll.vue'
  export default {
    name: 'HelloWorld',
    components: {
      scroll
    },
    data() {
      return {
        list: [],
        times: 1
      }
    },
    created() {
      for (let i = 0; i < 10; i++) {
        this.list.push('第' + this.times + '次的列表' + i)
      }
      this.times += 1
    },
    methods: {
      onLoad() {

        setTimeout(function() {
          for (let i = 0; i < 10; i++) {
            this.list.push('第' + this.times + '次的列表' + i)
          }
          this.times += 1
          this.$refs.pullBox.$el.style.transform="translateY(0px)"
          this.$refs.pullBox._data.scrollAble=true
        }.bind(this), 2000)
      }
    },
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .hello {
    width: 50%;
    position: absolute;
    left: 50%;
    top: 10%;
    transform: translate(-50%);
    height: 100px;
    overflow: hidden;
    background-color: #ddd;
  }
</style>
