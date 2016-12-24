<template>
  <div>
      <h2 style="text-align: center">现在是第{{current}}页</h2>
      <pagination :total="total" :current="current" :callback="changePage"></pagination>
  </div>
</template>

<script>
import pagination from './pagination/pagination.vue'
export default {
  data () {
    return {
      current:1,
      total:10
    }
  },
  components:{
    pagination
  },
  methods:{
    changePage:function(page){
      this.current = page;
      //分页操作这里
    }
  }
}
</script>

