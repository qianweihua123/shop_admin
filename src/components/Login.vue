<template>
  <div class="login">
    <el-form ref="form" :model="form" :rules="rules" label-width="80px" status-icon>
      <img src="@/assets/avatar.jpg" alt="">
      <el-form-item label="用户名" prop="username">
        <el-input v-model="form.username" placeholder="请输入用户名"></el-input>
      </el-form-item>
       <el-form-item label="密码" prop="password">
        <el-input v-model="form.password" placeholder="请输入密码" type="password"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="login">登录</el-button>
        <el-button @click="reset">重置</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
// 导入axios
import axios from 'axios'
export default {
  data () {
    return {
      form: {
        username: '',
        password: ''
      },
      // 表单的校验规则
      rules: {
        // 配置username的校验规则，可以有多个
        username: [
          // 必填的 trigger:blur 失去焦点的时候触发
          // trigger: change 改变的时候触发
          { required: true, message: '用户名不能为空', trigger: 'change' },
          { min: 3, max: 9, message: '长度在 3 到 9 个字符', trigger: 'change' }
        ],
        password: [
          // 必填的 trigger:blur 失去焦点的时候触发
          { required: true, message: '密码不能为空', trigger: 'change' },
          { min: 6, max: 12, message: '长度在 6 到 12 个字符', trigger: 'change' }
        ]
      }
    }
  },
  methods: {
    reset () {
      // 重置表单
      this.$refs.form.resetFields()
    },
    login () {
      this.$refs.form.validate(valid => {
        if (!valid) return false
        // 发送ajax请求  https://shop-api.circle.ink/
        axios({
          method: 'post',
          url: 'http://localhost:8888/api/private/v1/login',
          data: this.form
        }).then(res => {
          console.log(res.data)
          if (res.data.meta.status === 200) {
            // 使用提示信息  this.$message
            this.$message({
              message: '登录成功了',
              type: 'success',
              duration: 1000
            })
            // 把token给存储起来
            localStorage.setItem('token', res.data.data.token)
            // 转到首页组件
            // 类似于 location.href
            this.$router.push('/home')
          } else {
            this.$message.error(res.data.meta.msg)
            // this.$message({
            //   message: res.data.meta.msg,
            //   type: 'error'
            // })
          }
        })
      })
    }
  }
}
</script>

<style lang="less">
// lang="less": 表示使用less写css
.login {
  width: 100%;
  height: 100%;
  background-color: #2d434c;
  overflow: hidden;

  .el-form {
    width: 400px;
    background-color: #fff;
    margin: 200px auto;
    padding: 75px 40px 15px;
    position: relative;
    border-radius: 10px;
    img {
      position: absolute;
      left: 50%;
      transform: translateX(-50%);
      top: -70px;
      border-radius: 50%;
      border: 10px solid #fff;
    }

    .el-button ~ .el-button {
      margin-left: 80px;
    }
  }
}
</style>
