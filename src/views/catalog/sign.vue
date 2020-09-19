<template>
  <div class="catalog-index">
    <div class="page-title">签签签</div>

    <el-tabs type="border-card">
      <el-tab-pane>
        <span slot="label">
          <i class="iconfont iconhunyinlianai"></i> 婚姻签
        </span>
        <el-table
          :data="wedSigns.filter(data => !search || data.context.toLowerCase().includes(search.toLowerCase()))"
          style="width: 100%"
        >
          <el-table-column label="序号" prop="id"></el-table-column>
          <el-table-column label="签" prop="title"></el-table-column>
          <el-table-column label="内容" prop="context"></el-table-column>
          <el-table-column label="价值" prop="cost"></el-table-column>
          <el-table-column align="right">
            <template slot="header">
              <el-input v-model="search" size="mini" placeholder="输入关键字搜索" />
            </template>
            <template slot-scope="scope">
              <el-button size="mini" @click="handleEdit(scope.$index, scope.row)">Edit</el-button>
              <el-button
                size="mini"
                type="danger"
                @click="handleDelete(scope.$index, scope.row)"
              >Delete</el-button>
            </template>
          </el-table-column>
        </el-table>
      </el-tab-pane>
      <el-tab-pane>
        <span slot="label">
          <i class="iconfont iconMoneydollarfinancebusiness"></i> 事业签
        </span>
        <el-table
          :data="businessSigns.filter(data => !search || data.context.toLowerCase().includes(search.toLowerCase()))"
          style="width: 100%"
        >
          <el-table-column label="序号" prop="id"></el-table-column>
          <el-table-column label="签" prop="title"></el-table-column>
          <el-table-column label="内容" prop="context"></el-table-column>
          <el-table-column label="价值" prop="cost"></el-table-column>
          <el-table-column align="right">
            <template slot="header">
              <el-input v-model="search" size="mini" placeholder="输入关键字搜索" />
            </template>
            <template slot-scope="scope">
              <el-button size="mini" @click="handleEdit(scope.$index, scope.row)">Edit</el-button>
              <el-button
                size="mini"
                type="danger"
                @click="handleDelete(scope.$index, scope.row)"
              >Delete</el-button>
            </template>
          </el-table-column>
        </el-table>
      </el-tab-pane>
    </el-tabs>
  </div>
</template>

<script>
import $ from "jquery";

export default {
  name: "Sign",
  components: {},
  data() {
    return {
      signList: [],
      wedSigns: [],
      businessSigns: [],
      search: ""
    };
  },
  beforeCreate() {
    $.ajax({
      type: "GET",
      crossDomain: true,
      url: "https://localhost:44369/api/signList",
      dataType: "json",
      success: data => {
        console.log(data);
        this.signList = data;
        this.wedSigns = data.filter(sign => sign.type === "婚姻签");
        this.businessSigns = data.filter(sign => sign.type === "事业签");
      },
      error: err => {
        console.log("request json error" + err);
      }
    });
  },
  methods: {
    handleEdit(index, row) {
      console.log(index, row);
    },
    handleDelete(index, row) {
      console.log(index, row);
    },
    successCallback(data) {
      console.log(data);
    }
  }
};
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
