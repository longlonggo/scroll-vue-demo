<template>
    <ul :class="{'no-scroll':!scrollAble}" @touchstart="onTouchStart" @touchend="onTouchEnd" @touchmove="onTouchMove" @scroll="onScroll">
        <li v-for="(item, index) in list" :key="index">{{item}}</li>
    </ul>
</template>
<script>
export default {
    name: 'scroll',
    props: {
        list: Array
    },
    data() {
        return {
            beginX: 0,
            beginY: 0,
            lastY:0,
            touchMoveAble: false,
            scrollAble:true
        }
    },
    methods: {
        onTouchStart(e) {
              this.beginY = e.touches[0].screenY  
        },
        onTouchEnd() {
            this.lastY=this.returnTranslateY();
            if(this.lastY==-30){
                this.$emit('load')
            }
        },
        onTouchMove(e) {
            if(!this.touchMoveAble) return
            
            let Y = e.touches[0].screenY
            let y = Y - this.beginY
            y=this.lastY+y
            if(y<=-30){
                y=-30
            this.touchMoveAble=false
            }else if(y>=0){
                y=0
            }

            this.$el.style.transform="translateY("+y+"px)"
        },
        onScroll(){
            if(this.scrollAble){
                let h=this.list.length*20-100
                if(this.$el.scrollTop==h){
                    this.scrollAble=false
                    this.touchMoveAble=true;
                }
            }
        },
        returnTranslateY(){
            return 1*this.$el.style.transform.substring(11).split('p')[0]
        }
    }
}
</script>

<style>
    ul{
    width: 100%;
    background: skyblue;
    height: 100px;
    overflow-y: scroll;
  }
  .no-scroll{
    overflow-y: hidden;
  }
    li {
        width: 100%;
        height: 20px;
        background: red;
    }
</style>