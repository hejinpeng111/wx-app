<template>
  <div class="home">
      <!-- 背景头部 -->
      <img class="home-bg" :src="img.homeBg">

      <!-- 搜索框 -->

      <!-- 筛选按钮 -->
      <div class="home-filter">
          <div>
              <picker
                @change="cateChange"
                :value="curCate"
                range-key="label"
                :range="cates">
                <span v-text="cates[curCate].label"></span>
                <span>^</span>
              </picker>
          </div>
          <div></div>
          <div></div>
          <div></div>
      </div>
  </div>
</template>

<script>
    import card from '@/components/card'
    import img from '@/utils/img'
    import {goods} from '@/utils/data'
    
    export default{
        data() {
            return {
                img,
                curCate:0,
                cates:[
                    { id: 1, label: '手机数码', value: 'a' },
                    { id: 2, label: '母婴产品', value: 'b' },
                    { id: 3, label: '女士服装', value: 'c' },
                    { id: 4, label: '体育用品', value: 'd' }
                ],
                list:[]
            }
        },
        components:{
            card
        },
        // 下拉刷新
        onPullDownRefresh(){
            console.log("下拉刷新")
            this.list = goods
            setTimeout(()=>{
                mpvue.stopPullDownRefresh()
            },2000)
        },

        // 分页
        onReachBottom(){
            this.list = [...this.list,...goods]
        },

        // 掉接口
        onShow(){
            this.list = goods
        },

        methods: {
            bindViewTap(){
                const url = '../logs/main'
                if(mpvuePlatform === wx){
                    mpvue.switchTab({url})
                }else{
                    mpvue.navigateTo({url})
                }
            },
            clickHandle(ev){
                
            }
        },
    }

</script>

<style scoped>

</style>
