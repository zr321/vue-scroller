<template>
  <div class="hellWorld">
    <scroller :on-refresh="refresh" :on-infinite="infinite" ref="myscroller">
      <ul>
        <li v-for="(m,i) in moveList" :key="i">{{m}}</li>
      </ul>
    </scroller>
  </div>
  
</template>
<script>
export default {
  data(){
    return{
      noData: '',
      moveList: 
      [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20]  
    }
  },
  methods:{
    infinite(done) {//往后刷新增加内容
      if(this.noData) {
        setTimeout(()=>{
          this.$refs.myscroller.finishInfinite(2);
        })
        return;
      }
      let self = this;//this指向问题
      let start = this.moveList.length;

      setTimeout(() => {
        for(let i = start + 1; i < start + 10; i++) {
          self.moveList.push(i)
        }
        if(start > 30) {
          self.noData = "没有更多数据"
        }
        self.$refs.myscroller.resize();
          done()
      }, 1500)
  },

  //done()表示这次异步加载数据完成，加载下一次
  //因为这个是同步的，加了setTimeout就是异步加载数据；
  //因为涉及到this指向问题，所以将他放在一个变量里。
  refresh (done) {//往前刷新增加内容
        setTimeout(() => {
          var start = this.moveList.length - 1
          for (var i = start; i > start - 10; i--) {
            this.moveList.splice(0, 0, i + '刷新数据')
          }
          done()
        }, 1500)
    }
  }
}
</script>
<style lang="less">
  *{
    margin:0;padding:0;
  }
  html,body{
    margin:0;
    font-size: 16px;
  }
  .hellWorld{
    margin:0;
    ul,li{
      list-style: none;
    }
    li{
      height: 40px;
      line-height: 40px;
      background: #ddd;
      margin-bottom:10px;
    }
  }
  
</style>
