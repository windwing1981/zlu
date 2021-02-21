<template>
  <el-container>
    <el-header>
      <el-container>
        <h2>hello,zlu!&nbsp;&nbsp;&nbsp;</h2>
        <el-button @click="dialogVisible = true" >点击打开 Dialog</el-button>
        <div>
          <el_recipe :dialogstate="dialogVisible" @closed="closed"></el_recipe>
        </div>
      </el-container>
    </el-header>
    <el-main>
      <el-table
        :data="tableData"
        @cell-dblclick="celledit"
        style="width: 100%">
        <el-table-column
          prop="date"
          label="日期"
          width="180">
        </el-table-column>
        <el-table-column
          prop="name"
          label="姓名"
          width="180">
          <template slot-scope="scope">
              <el-input v-if="scope.row.isOK" v-model="scope.row.name" style="width:100%;hight:100%"></el-input>
              <span v-else>{{scope.row.name}}</span>
        </template>
        </el-table-column>
        <el-table-column
          prop="address"
          label="地址">
        </el-table-column>
      </el-table>
    </el-main>
  </el-container>  
</template>

<script>
import el_recipe from '../components/el_recipe.vue'

export default {
  data () {
    return {
      dialogVisible: false,
      tableData: [{
            date: '2016-05-02',
            name: '王小虎123',
            isOK: true,
            address: '上海市普陀区金沙江路 1518 弄'
          }, {
            date: '2016-05-04',
            name: '王小虎456',
            isOK: true,
            address: '上海市普陀区金沙江路 1517 弄'
          }, {
            date: '2016-05-01',
            name: '王小虎789',
            isOK: true,
            address: '上海市普陀区金沙江路 1519 弄'
          }, {
            date: '2016-05-03',
            name: '王小虎',
            isOK: true,
            address: '上海市普陀区金沙江路 1516 弄'
          }]
    }
  },
  components : {el_recipe},
  methods:{
    closed(){
      this.dialogVisible=false
    },
    celledit(row, column,cell,event){
      row.isOK =!row.isOK
    },

  }
}
</script>