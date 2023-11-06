<template>
  <div>
    <!-- 搜索栏 -->
    <el-card id="search">
      <el-row>
        <el-col :span="20">
          <el-input v-model="searchModel.id" placeholder="ID"></el-input>
          <el-input v-model="searchModel.date" placeholder="日期"></el-input>
          <el-input v-model="searchModel.location" placeholder="地理位置"></el-input>
          <el-button type="primary" round icon="el-icon-search">查询</el-button>
        </el-col>
        <el-col :span="4" align="right">
          <el-button @click="openEditUI" type="primary" icon="el-icon-plus" circle></el-button>
        </el-col>
      </el-row>
    </el-card>

    <!-- 表格 -->
    <el-card>
      <el-table :data="earthquakeSituation" style="width: 100%">
        <el-table-column type="index" label="#" width="50"> </el-table-column>
        <el-table-column prop="id" label="id" width="120"> </el-table-column>
        <el-table-column prop="date" label="日期" width="120">
        </el-table-column>
        <el-table-column prop="address" label="地理位置" width="120">
        </el-table-column>
        <el-table-column prop="longitude" label="经度" width="80">
        </el-table-column>
        <el-table-column prop="latitude" label="纬度" width="80">
        </el-table-column>
        <el-table-column prop="depth" label="震源深度" width="80">
        </el-table-column>
        <el-table-column prop="magnitude" label="震级" width="80">
        </el-table-column>
        <el-table-column prop="picture" label="图像" width="180">
        </el-table-column>
        <el-table-column prop="workunit" label="上报单位" width="180">
        </el-table-column>
        <el-table-column label="操作">
          <template slot-scope="scope">
            <el-button size="mini" @click="handleEdit(scope.$index, scope.row)">编辑</el-button>
            <el-button
              size="mini"
              type="danger"
              @click="handleDelete(scope.$index, scope.row)"
              >删除</el-button
            >
          </template>
        </el-table-column>
      </el-table>
    </el-card>

    <!-- 分页 -->
    <el-pagination
      @size-change="handleSizeChange"
      @current-change="handleCurrentChange"
      :current-page="searchModel.pageNo"
      :page-sizes="[10, 20, 30, 40]"
      :page-size="searchModel.pageSize"
      layout="total, sizes, prev, pager, next, jumper"
      :total="total"
    >
    </el-pagination>

    
  </div>
</template>

<script>
export default {
  data() {
    return {
      formLabelWidth: '130px',
      userForm: {},
      dialogFormVisible: false,
      title:"",
      total: 0,
      searchModel: {
        pageNo: 1,
        pageSize: 10,
      },
      earthquakeSituation: [],
    };
  },
  methods: {
    openEditUI(){
      this.title= '新增用户';
      this.dialogFormVisible= true;
    },
    handleCurrentChange() {},
    handleSizeChange() {},
  },
};
</script>

<style>
#search .el-input {
  width: 200px;
  margin-right: 20px;
}
</style>