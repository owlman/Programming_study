<template>
    <div id="tab-sign" class="tab-content">
        <table>
            <tr>
                <td>请输入用户名：</td>
                <td><input type="text" v-model="userName"></td>
            </tr>
            <tr>
                <td>请设置密码：</td>
                <td><input type="password" v-model="password"></td>
            </tr>
            <tr>
                <td>请重复密码：</td>
                <td><input type="password" v-model="rePassword"></td>
            </tr>
            <tr>
                <td><input type="button" value="注册" @click="signUp"></td>
                <td><input type="button" value="重置" @click="reset"></td>
            </tr>
        </table>
    </div>
</template>

<script>
    import axios from 'axios';

    export default {
        name: "tab-sign",
        data() {
            return {
                userName: '',
                password: '',
                rePassword: ''
            };
        },
        methods: {
            signUp: function() {
                if(this.userName !== '' &&
                   this.password !== '' &&
                   this.rePassword !== '') {
                       if(this.password === this.rePassword) {
                           const that = this;
                           axios.post('/user/sign', {
                               userName: that.userName,
                               password: that.password
                           })
                           .then(function(res) {
                               console.log(res.statusText)
                               if(res.statusText === 'OK') {
                                    window.alert(res.data);
                                    that.reset();
                               }
                           })
                           .catch(function() {
                               window.alert('注册请求失败！')
                           });
                       } else {
                           window.alert('你两次输入的密码不一致！');
                       }
                   } else {
                       window.alert('请正确填写注册信息！');
                   }

            },
            reset: function() {
                this.userName = '';
                this.password = '';
                this.rePassword = '';
            }
        }
    };
</script>

<style scoped>
</style>