<script setup>
import axios from 'axios';
import {ref} from 'vue'
import {useRouter} from 'vue-router'
import {createRouter, createWebHistory} from "vue-router";
import HomeView from '../views/HomeView.vue'
import LoginView from '../views/LoginView.vue'
import qs from 'querystring'

let username = ref('')
let password = ref('')
const router = useRouter();

function handleClick() {/*
console.log(username.value);
  let data = {
    username: username.value,
    password: password.value
  }
  axios.post('http://localhost:8080/hit/user/login', qs.stringify(data))
      .then((res) => {
        console.log(res.data)
        if (res.data.success) {
          console.log("success")

        } else {
          console.log("login fail")
        }
      })
      .catch((err) => {
        console.log(err)
      })
}*/

  if (username.value === 'admin' && password.value === '123') {
    sessionStorage.setItem("username", username.value);
    router.replace('/');
  }
}

</script>


<template>
  <el-input
      v-model="username"
      style="width: 240px"
      placeholder="用户名"
  />
  <br>
  <el-input
      v-model="password"
      type="password"
      style="width: 240px"
      placeholder="密码"
      show-password
  />
  <br>
  <el-button type="primary" @click="handleClick">登录</el-button>
</template>
