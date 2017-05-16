<template>
    <div>
      <form>
        <div class="form-group">
          <label for="bookName" class="control-label">书名</label>
          <input type="text" id="bookName" class="form-control" autocomplete="off" v-model="book.bookName">
        </div>
        <div class="form-group">
          <label for="bookCover" class="control-label">封面</label>
          <input type="text" id="bookCover" class="form-control" autocomplete="off" v-model="book.bookCover">
        </div>
        <div class="form-group">
          <label for="bookPrice" class="control-label">价格</label>
          <input type="text" id="bookPrice" class="form-control" autocomplete="off" v-model="book.bookPrice">
        </div>
        <div class="form-group">
          <button type="button" class="btn btn-primary" @click="add">添加图书</button>
        </div>
      </form>
    </div>
</template>
<script>
    export default {
        data(){
            return {book:{
                bookName:'',
                bookPrice:'',
                bookCover:''
            }}
        },
        components: {},
        methods: {
            add(){
                this.$http.post('/book',this.book).then(()=>{
                    this.$router.push('/list');
                });
            }
        }
    }
</script>
<style scoped>

</style>
