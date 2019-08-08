<template>
  <div>
    <el-row class="nameTop" type="flex" justify="center" align="middle">
      <el-col :span="22"><h1>{{name}}</h1></el-col>
      <el-col :span="2"><i class="el-icon-delete-solid" @click="deleteTodo"></i></el-col>
    </el-row>
    <el-row>
      <el-col :span="22">
        <el-input v-model="input" placeholder="请输入内容"></el-input>
      </el-col>
      <el-col :span="2">
        <el-button type="primary" @click="add">增加 <i class="el-icon-circle-plus-outline"></i></el-button>
      </el-col>
    </el-row>
  </div>
</template>
<script>
  export default{
    props: {
      name: {
        type: Object
      }
    },
    data(){
      return {
        input: ''
      }
    },
    methods: {
      add(){
        this.$emit('addItem', this.input)
        this.input = ''
      },
      deleteTodo(){
          this.$emit('deletetodo')
      }
    }
  }
</script>
<style>
.nameTop{
  height:60px;
  line-height:60px;
  background: #fff;
}
</style>
