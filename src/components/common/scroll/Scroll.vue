<template>
    <div class="wrapper" ref="wrapper">
        <div class="content">
            <slot></slot>
        </div>
    </div>
</template>

<script>
import BScroll from 'better-scroll'
export default {
    name:"Scroll",
    data() {
        return {
            scroll:null
        }
    },
    props: {
        probeType: {
            type: Number,
            default: 0
        },
        pullUpLoad: {
            type: Boolean,
            default: false
        }
    },
    methods: {
        scrollTo(x, y, time=300) {
            this.scroll && this.scroll.scrollTo(x, y, time)
        },
        finishPullUp() {
            this.scroll && this.scroll.finishPullUp()
        },
        refresh() {
            // console.log("--------")
            this.scroll && this.scroll.refresh()
      }
    },
    mounted() {
        // 1.创建BScroll对象
        this.scroll = new BScroll(this.$refs.wrapper,{
            click: true,
            probeType: this.probeType,
            pullUpLoad: this.pullUpLoad
        })

        this.scroll.on('scroll',(position) => {
            // console.log(position)
            this.$emit('scroll', position)

            // console.log(this.scroll)
            // 解决了滚动的bug
            // this.scroll.refresh()
        })
        if(this.pullUpLoad){
            this.scroll.on('pullingUp',() => {
            // console.log('上拉加载更多')
            this.$emit('pullingUp')
            })
        }   
    }
}
</script>

<style scoped>

</style>