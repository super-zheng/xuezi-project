<template>
  <div>
      <!-- page content -->
        <div class="row">
          <div class="col-xs-12 x_title">
            <h3>用户列表</h3>
          </div>
        </div>
        <div class="row">
          <div class="col-xs-3">
            <form class="form-inline">
              <div class="form-group">
                <label for="page-size">每页显示记录数：</label>
                <select class="form-control" id="page-size">
                  <option value="10">10</option>
                  <option value="20">20</option>
                  <option value="40">40</option>
                  <option value="60">60</option>
                  <option value="80">80</option>
                  <option value="100">100</option>
                </select>
              </div>
            </form>
          </div>
          <div class="col-xs-4 col-xs-offset-5">
            <div class="form-group has-feedback">
              <label for="product-kw" class="sr-only">搜索关键字：</label>
              <input class="form-control" type="text" id="product-kw" placeholder="请输入搜索关键字">
              <span class="glyphicon glyphicon-search form-control-feedback"></span>
            </div>
          </div>
        </div>
        <div class="row">
          <div class="col-xs-12">
            <div class="table-responsive">
              <table class="table table-hover table-striped" id="table-laptop">
                <thead>
                <tr>
                  <th>
                    <div class="checkbox" style="margin: 0;">
                      <label>
                        <input type="checkbox">全选
                      </label>
                    </div>
                  </th>
                  <th>编号</th>
                  <th>头像</th>
                  <th>登录名</th>
                  <th>用户名</th>
                  <th>性别</th>
                  <th>邮箱</th>
                  <th>电话</th>
                  <th>操作</th>
                </tr>
                </thead>
                <tbody>
                <tr v-if="list.length==0">
                  <td colspan="8">
                    <div class="loading">
                      <img src="../assets/img/loading.gif" alt="">
                    </div>
                  </td>
                </tr>
                <tr v-for="users in list">
                  <td><input type="checkbox"></td>
                  <td>{{users.uid}}</td>
                  <td><img
                    style="width: 70px;height:70px"
                    class="pic"
                    :src="require('../assets/'+users.avatar)"></td>
                  <td><p>{{users.uname}}</p></td>
                  <td><p>{{users.user_name}}</p></td>
                  <td><p>{{users.gender}}</p></td>
                  <td><p>{{users.email}}</p></td>
                  <td>{{users.phone}}</td>
                  <td>
                    <a href="product_details.html">详情</a>
                    <a href="product_update.html">修改</a>
                    <a href="product_delete.html">删除</a>
                  </td>
                </tr>
                </tbody>
              </table>
            </div>
            <div class="row">
              <div class="col-xs-12">
                <ul class="pagination pull-right" id="pagination">
                  <li><a href="#">上一页</a></li>
                  <li><a href="#">1</a></li>
                  <li><a href="#">2</a></li>
                  <li class="active"><a href="#">3</a></li>
                  <li><a href="#">4</a></li>
                  <li><a href="#">5</a></li>
                  <li><a href="#">下一页</a></li>
                </ul>
              </div>
            </div>
          </div>
        </div>
        <br>
      <!-- /page content -->

      <!-- footer content -->


  </div>
</template>

<script>
  export default{
    data:function () {
      return {
          list:[]
      }
    },
    methods:{
      loadUsers:function () {
        this.$http.get("http://127.0.0.1/admin/data/user_list.php")
          .then((response)=>{
            console.log(response.data);
            this.list =
              response.data.data;
          })
      }
    },
    created: function () {
      //向服务器端获取商品列表的数据
      this.loadUsers();
    }
  }
</script>
