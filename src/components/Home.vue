<template>
 <div class="home">
   <el-container>
  <el-header>
    <div class="logo"></div>
    <div class="title">
      <h1>电商后台管理系统</h1>
    </div>
    <div class="logOut">
      <span>欢迎光临</span><a href="javascript:;" @click="loginOut">退出</a>
    </div>
  </el-header>
  <el-container>
    <el-aside width="200px">Aside</el-aside>
    <el-main>Main</el-main>
  </el-container>
</el-container>
 </div>
</template>

<script>
export default {
  methods: {
    loginOut () {
      this.$confirm('您确定要退出本系统吗？', '温馨提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      }).then(() => {
        localStorage.removeItem('token')
        this.$router.push('/login')
        this.$message({
          type: 'success',
          message: '退出成功!'
        })
      }).catch(() => {
        this.$message({
          type: 'info',
          message: '已取消退出'
        })
      })
    }
  }
}
</script>

<style lang = "less" scoped>
 .home{
   height:100%;
   .el-container{
    height: 100%;
   }

   .el-header{
     background-color: #B3C1CD;
     display: flex;
     .logo{
      width: 180px ;
      background-image: url('~@/assets/logo.png');
      background-size: contain;
      background-repeat: no-repeat;
      background-position: center center;
     }
     .logOut{
       width: 180px;
       line-height: 60px;
       text-align: right;
       font-weight: bolder;
       a{
         color: #FF8C40;
       }
     }
     .title{
       flex: 1;
       h1{
       text-align: center;
       line-height: 60px;
       color: white;
       font-size: 30px;
       }
     }
   }
   .el-aside{
     background-color: #545C64;
   }
   .el-main{
     background-color: #D4DFE4;
   }
 }
</style>
