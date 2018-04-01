<template>
  <div class="login-wrapper">
    <div class="login-content">
      <Card :bordered="false">
        <p slot="title">
          <Icon type="log-in"></Icon>
          欢迎登录
        </p>
        <div class="form-con">
          <Form ref="user" :model="user" :rules="ruleInline">
            <FormItem prop="name">
              <Input v-model="user.name" placeholder="请输入用户名">
              <span slot="prepend">
                     <Icon :size="16" type="person"></Icon>
              </span>
              </Input>
            </FormItem>
            <FormItem prop="password">
              <Input type="password" v-model="user.password" placeholder="请输入密码">
              <span slot="prepend">
                <Icon :size="14" type="locked"></Icon>
              </span>
              </Input>
            </FormItem>
            <FormItem>
              <Button @click="login('user')" type="primary" long>登录</Button>
            </FormItem>
          </Form>
          <p class="login-tip">用户名和密码:admin/admin</p>
        </div>
      </Card>
    </div>
  </div>
</template>
<script>
  export default {
    name:'login',
    data(){
      return {
        user:{
          name:'',
          password:''
        },
        ruleInline: {
          name: [
            { required: true, message: '请输入用户名', trigger: 'blur' }
          ],
          password: [
            { required: true, message: '请输入密码', trigger: 'blur' },
            { type: 'string', min: 4, message: '密码不能少于四位', trigger: 'blur' }
          ]
        }
      }
    },
    methods:{
      login(name){
        this.$refs[name].validate((valid) => {
          if (valid) {
            this.$Message.success('Success!');
            this.$router.push({
              name: 'HelloWorld'
            });
          } else {
            this.$Message.error('Fail!');
          }
        })
      }
    }
  }
</script>

<style lang="scss">
  .login-wrapper{
     background-image: url('../assets/images/login_bg.jpg');
    height: 100%;
    width: 100%;
    background-size: cover;
    .login-content{
      height: 273px;
      width: 300px;
      background-color: aliceblue;
      right: 150px;
      top: calc(50% - 150px);
      position: absolute;
      border-radius: 4px;
    }

  }
</style>
