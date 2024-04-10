<script setup>
import axios from 'axios';
import {ref} from 'vue'
import {useRouter} from 'vue-router'
import qs from 'querystring'
let username = ref('')
let password = ref('')
const router = useRouter();

function handleLogin(){
    let data = {
    username: username.value,
    password: password.value
}
    axios.post("http://localhost:8080/login",qs.stringfy(data))
    .then((res) => {
        sessionStorage.setItem("username", username);
        router.replace('/')
    })
    .catch((err) => {
        console.log(err)
    })
}
    if(username.value === 'admin' && password.value === '123'){
        sessionStorage.setItem("username", username);
        router.replace('/');
    
    }

</script>


<template>
    <el-input v-model="username" style="width: 240px" placeholder="用户名" /><br>
    <el-input v-model="password" type="password" style="width: 240px" placeholder="密码" /><br>
    <el-button type="primary" @click="handleLogin">登录</el-button>
</template>
