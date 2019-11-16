<template>
  <div>
    <el-table ref="multipleTable" :data="goodsList" style="max-width:80vw">
      <el-table-column type="selection"></el-table-column>
      <el-table-column prop="id" label="商品编号"></el-table-column>
      <el-table-column label="商品图片">
        <template slot-scope="scope">
          <img :src="scope.row.imgsrc" alt style="width: 50px;height: 50px" />
        </template>
      </el-table-column>
      <el-table-column prop="name" label="商品名称"></el-table-column>
      <el-table-column prop="price" label="商品价格"></el-table-column>
      <el-table-column prop="type" label="商品类别"></el-table-column>
      <el-table-column prop="level" label="商品品质"></el-table-column>
      <el-table-column prop="desc" label="描述"></el-table-column>
      <el-table-column label="操作">
        <template slot-scope="scope">
          <el-button size="mini" @click="handleEdit(scope.$index,scope.row)">编辑</el-button>
          <el-button size="mini" type="danger" @click="delGoods(scope.row)">删除</el-button>
        </template>
      </el-table-column>
    </el-table>
    <div style="text-align:center">
      <el-pagination
        background
        :page-size="pageSize"
        layout="prev, pager, next"
        @current-change="getGoodsList()"
        :total="goodsPages"
      ></el-pagination>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // loading: false,
      goodsList: [],
      pageSize: 5,
      goodsPages: 0
    };
  },
  methods: {
    // delGoods(row) {
    //   this.$confirm(`确定删除${row.name}吗?`, "提示", {
    //     type: "warning"
    //   }).then(() => {
    //     //删除数据
    //     this.$axios
    //       .post("http://romove", {
    //         id: row.id
    //       })
    //       .then(res => {
    //         if (res.date.success) {
    //           this.$success("删除成功!");
    //           this.getGoodsList();
    //         } else {
    //           this.$fail("删除失败!");
    //         }
    //       });
    //   });
    // },
    //获取页数
    // getGoodspages() {
    //   this.$axios.get().then(res => {
    //     this.goodsPages = res.date.count;
    //   });
    // },
    // getGoodsList(pageIdx = 1) {
    getGoodsList() {
      // console.log(pageIdx);
      // this.loading = true;
      // this.getGoodspages();
      // 发送请求拿数据
      this.$axios
        .get(
          "http://localhost:1910/goods"
          // , {
          //   params: {
          //     pageIdx,
          //     pageSize: 5
          //   }
          // }
        )
        .then(res => {
          console.log(res.data.data);
          this.goodsList = res.data.data;
          // this.loading = false;
        });
    }
  },
  created() {
    this.getGoodsList();
  }
};
</script>

<style>
</style>