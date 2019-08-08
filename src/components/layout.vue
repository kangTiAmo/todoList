<template>
  <div>
    <el-container>
      <el-header style="background: -webkit-gradient(linear, left top, left bottom, from(#d0edf5), to(#e1e5f0));
background: linear-gradient(to bottom, #d0edf5, #e1e5f0 100%);height: 100%;">
        <Head></Head>
      </el-header>
      <el-container>
        <el-aside width="400px" style="">
          <Todo :todoList="todoList" @getId="getId" @addTodo="addTodo"></Todo>
        </el-aside>
        <el-main style="padding: 0;">
          <AddItem @addItem="addItem" :name="nowName" @deletetodo="deleteTodo"></AddItem>
          <Item :items="List"></Item>
        </el-main>
      </el-container>
    </el-container>
  </div>
</template>

<script>
  import Head from './headder.vue';
  import Todo from './todo.vue';
  import Item from './item.vue';
  import AddItem from './addItem.vue';
  import Mock from 'mockjs'
  export default {
    data(){
      return {
        List: [],
        todoList: [],
        nowId: '',
        nowName:''
      }
    },
    created(){
      this.getlist()
    },
    methods: {
      getTime(){
        let date = new Date();
        var seperator1 = "-";
        var year = date.getFullYear();
        var month = date.getMonth() + 1;
        var strDate = date.getDate();
        if (month >= 1 && month <= 9) {
          month = "0" + month;
        }
        if (strDate >= 0 && strDate <= 9) {
          strDate = "0" + strDate;
        }
        var currentdate = year + seperator1 + month + seperator1 + strDate;
        return currentdate;
      },
      getId(data){
        this.List = this.todoList[data].items
        this.nowId = data;
        this.nowName = this.todoList[data].title;

      },
      addItem(data){
        this.todoList[this.nowId].items.push({
          date: this.getTime(),
          content: data
        })
      },
      deleteTodo(){
          this.todoList.splice(this.nowId,1);
          this.getId(0)
      },
      getlist(){
        const count = [1, 2, 3, 4, 5, 6];
        for (let i = 0; i < count.length; i++) {
          this.todoList.push({
              id: Mock.Random.guid(),
              title: Mock.Random.sentence(1),
              items: count.map(() => {
                return {
                  date: Mock.Random.date('yyyy-MM-dd'),
                  content: Mock.Random.csentence()
                }
              })
            }
          )
        }
        //console.log(this.todoList)
      },
      addTodo(data){
        this.todoList.push({
          id: Mock.Random.guid(),
          title: data,
          items:[]
        })
      }
    },
    components: {
      Head,
      Todo,
      Item,
      AddItem
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->

<style>

</style>
