<template>
    <div class="catalog-index">
        <h4 class="page-title">签签签</h4>

        <el-tabs type="border-card">
            <el-tab-pane>
                <span slot="label"><i class="iconfont iconhunyinlianai"></i> 婚姻签</span>
                婚姻签
                <el-table
                        :data="tableData.filter(data => !search || data.name.toLowerCase().includes(search.toLowerCase()))"
                        style="width: 100%">
                    <el-table-column
                            label="Date"
                            prop="date">
                    </el-table-column>
                    <el-table-column
                            label="Name"
                            prop="name">
                    </el-table-column>
                    <el-table-column
                            align="right">
                        <template slot="header">
                            <el-input
                                    v-model="search"
                                    size="mini"
                                    placeholder="输入关键字搜索"/>
                        </template>
                        <template slot-scope="scope">
                            <el-button
                                    size="mini"
                                    @click="handleEdit(scope.$index, scope.row)">Edit
                            </el-button>
                            <el-button
                                    size="mini"
                                    type="danger"
                                    @click="handleDelete(scope.$index, scope.row)">Delete
                            </el-button>
                        </template>
                    </el-table-column>
                </el-table>

            </el-tab-pane>
            <el-tab-pane>
                <span slot="label"><i class="iconfont iconMoneydollarfinancebusiness"></i> 事业签</span>
                事业签
            </el-tab-pane>
        </el-tabs>

    </div>
</template>

<script>

  import $ from 'jquery'

  export default {
    name: 'Sign',
    components: {},
    data () {
      return {
        tableData: [{
          date: '2016-05-02',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          date: '2016-05-04',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1517 弄'
        }, {
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1519 弄'
        }, {
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1516 弄'
        }],
        search: ''
      }
    },
    beforeCreate () {
      $.ajax({
        type: "GET",
        crossDomain: true,
        url: 'https://localhost:44369/api/signList',
        dataType: "json",
        success: data => {
          console.log(data)
        },
        error: (err) => {
          console.log('request json error' + err)
        }
      })
    },
    methods: {
      handleEdit (index, row) {
        console.log(index, row)
      },
      handleDelete (index, row) {
        console.log(index, row)
      },
      successCallback(data) {
        console.log(data)
      }
    },
  }
</script>

<style lang="less" scoped>
    .right-panel {
        padding: 15px;
        background-color: #faf9f3;
        min-height: calc(~"100vh - 262px");
        border-left: 1px solid #f1f1f1;
    }

    span {
        font-size: 14px;

        i {
            margin: 0 5px;
        }
    }
</style>
