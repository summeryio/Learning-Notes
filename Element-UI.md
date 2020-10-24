##### Form 表单提交/关闭时清空

```
this.$refs[form].resetFields();
```



##### select 选择时获取其他参数，参考后台管理-薪资模板





##### 在弹框编辑中，给form设置数据时，要用...去赋值



##### Chrome浏览器登录页input填充背景色

```
// login/index.vue
.login-container {
  .el-input {
    input {
      &:-webkit-autofill { // 如下设置
        -webkit-box-shadow: 0 0 0px 1000px white inset !important;
        box-shadow: 0 0 0px 1000px white inset !important;
      }
    }
  }
```

