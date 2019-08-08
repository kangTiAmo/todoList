<template>
  <el-card class="box-card">
    <div @click="goList(key)" class="text" :class="{active:isChoose===key}" v-for="(item,key) in todoList">
      <el-row>
        <el-col :span="22">{{item.title}}</el-col>
        <el-col :span="2">
          <el-badge :value="item.items.length"></el-badge>
        </el-col>
      </el-row>
    </div>
      <div class="text">
        <el-button type="text" @click="addTodo" style="width: 100%">
        <el-row>
          <el-col :span="24"><i class="el-icon-plus"></i>增加</el-col>
        </el-row>
        </el-button>
      </div>
  </el-card>
</template>
<script>
  export default{
    props: {
      todoList: {
        type: Object
      }
    },
    data(){
      return {
        isChoose: 0
      }
    },
    created(){
      this.goList(0)
    },
    methods: {
      goList(id){
        this.isChoose = id;
        this.$emit('getId', id)
      },
      addTodo(){
        this.$prompt('请输入名称', '提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          inputPattern: /\S/,
          inputErrorMessage: '名称不能为空'
        }).then(({ value }) => {
          this.$message({
            type: 'success',
            message: '你的输入是: ' + value
          });
          this.$emit('addTodo', value)
          this.goList(this.todoList.length-1)
        }).catch(() => {
          this.$message({
            type: 'info',
            message: '取消输入'
          });
        });
      }
    },
    watch:{
        'todoList':{
          handler(newName, oldName){
            this.isChoose = 0
          }
        },
      deep:true
    }
  }
</script>
<style>
  .text {
    border-bottom: 1px solid #ccc;
    height: 60px;
    line-height: 60px;
    color: #999;
    cursor: pointer;
  }

  .el-badge__content {
    background-color: #999;
  }

  .active {
    color: #333;
  }

  .active .el-badge__content {
    background-color: #2cc5d2;
  }

  .text:hover {
    color: #333;
  }

  .text:hover .el-badge__content {
    background-color: #2cc5d2;
  }
</style>
