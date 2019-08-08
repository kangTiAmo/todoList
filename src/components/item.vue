<template>
  <div>
    <el-table
      :data="items"
      style="width: 100%" fit>
      <el-table-column
        label="日期" width="200">
        <template slot-scope="scope">
          <i class="el-icon-time"></i>
          <span style="margin-left: 10px">{{ scope.row.date }}</span>
        </template>
      </el-table-column>
      <el-table-column
        label="内容" align="center">
        <template slot-scope="scope">
          <span>{{scope.row.content}}</span>
        </template>
      </el-table-column>
      <el-table-column label="操作" align="center">
        <template slot-scope="scope">
          <el-button
            size="mini"
            @click.native.prevent="show(scope.$index,items)">编辑
          </el-button>
          <el-dialog title="修改内容" :visible.sync="dialogFormVisible">
            <el-form :model="form">
              <el-form-item label="内容" width="120px">
                <el-input v-model="form.name" clearable></el-input>
              </el-form-item>
            </el-form>
            <div slot="footer" class="dialog-footer">
              <el-button @click="dialogFormVisible = false">取 消</el-button>
              <el-button type="primary" @click="updata()">确 定</el-button>
            </div>
          </el-dialog>
          <el-button
            size="mini"
            type="danger"
            @click.native.prevent="deleteRow(scope.$index, items)">删除
          </el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>
<script>
  export default{
    props: {
      items: {
        type: Object
      }
    },
    data(){
      return {
        form: {
          name: ''
        },
        dialogFormVisible: false,
        nowIndex:''
      }
    },
    methods: {
      deleteRow(index, rows) {
        rows.splice(index, 1);
      },
      show(index,row){
        this.dialogFormVisible = true;
         this.form.name = this.items[index].content
          this.nowIndex = index;
      },
      updata(){
          console.log(this.items,this.nowIndex)
        this.items[this.nowIndex].content = this.form.name;
        this.dialogFormVisible = false;
        this.form.name = ""
      }
    }
  }
</script>
<style>

</style>
