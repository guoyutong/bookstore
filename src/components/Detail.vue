<template>
  <div>
    <div>
      <div class="panel panel-warning">
        <div class="panel-heading">
          书名:<span v-show="!flag">{{book.bookName}}</span>
          <input type="text" v-model="book.bookName" v-show="flag">
        </div>
        <div class="panel-body text-center">
          <img :src="book.bookCover" alt="">
        </div>
        <div class="panel-footer">
          <span v-show="!flag">价格:{{book.bookPrice | currency('￥')}}</span>
          <input type="text" v-model="book.bookPrice" v-show="flag">
          <button class="btn btn-danger" @click="remove" v-show="!flag">删除</button>
          <button class="btn btn-warning" @click="changeFlag" v-show="!flag">修改</button>
          <button class="btn btn-primary" @click="update" v-show="flag">确认</button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
  export default {
    filters:{
      currency(input,param1){
        //input代表的是book.bookPrice
        return param1 + input;
      }
    },
    created(){
      //页面已加载，就需要获取数据，获取id对应的数据
      this.id = this.$route.params.id;
      this.$http.get('/book?id='+this.id).then(res=>{
          this.book = res.body;
      })
    },
    data(){
      return {
        book:{
            bookName:'',
          bookPrice:'',
          bookCover:''
        },
        id:'',
        flag:false//默认不显示输入框
      }
    },
    components: {},
    methods: {
      remove(){
          this.$http.delete('/book?id='+this.id).then(()=>{
              this.$router.push('/list');//push路由跳转
          })
      },
      changeFlag(){
          this.flag = !this.flag;
      },
      update(){
        //通过url传递id，数据通过请求体传
        //服务端只要调用res.end就会触发成功的回调
        this.$http.put('/book?id='+ this.id,this.book).then(()=>{
            this.flag = false;//vue-resouce将then中的this处理掉了，默认执行当前组件
        })
      }
    }
  }
</script>
<style scoped>
  img{
    width: 150px;
    height: 200px;
  }
</style>
