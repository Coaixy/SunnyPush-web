<script setup>
import { onMounted, ref } from 'vue';
import Login from './Componet/Login.vue';
import DataTable from './Componet/DataTable.vue';
const url = "http://103.205.253.197:401/"
let isLogin = ref(false);
let tableData = ref([]);
onMounted(() => {
  let user_name = localStorage.getItem("user_name")
  let user_pwd = localStorage.getItem("user_pwd")
  if (user_name != null && user_pwd != null) {
    if (isBlank(localStorage.getItem("session"))) {
      get_session(user_name, user_pwd)
    }
    get_data()
  }
});

function get_data() {
  console.log(localStorage.getItem("session"))
  const session_id = localStorage.getItem("session")
  console.log(session_id)
  const data_url = url + "get_data?session_id=" + session_id
  fetch(data_url).then(response => response.json()).then(data => {
    if (data.msg == "Get Success" && data.data != null) {
      tableData.value = data.data
      login()
    } else {
      logout()
    }
  })
}
function get_session(user_name, user_pwd) {
  const session_url = url + "get_session?user_name=" + user_name + "&user_pwd=" + user_pwd
  fetch(session_url).then(response => response.json()).then(data => {
    if (data.msg == "Get Success") {
      localStorage.setItem("session", data.session_id)
      get_data()
      login()
    } else {
      logout()
    }
  })
}
function login() {
  isLogin.value = true
  console.log("触发登录")
}
function logout() {
  isLogin.value = false
  localStorage.setItem("session", null)
  console.log("触发登出")
}
function isBlank(data) {
  if (
    data == null ||
    data === 'null' ||
    data === '' ||
    data === undefined ||
    data === 'undefined' ||
    data === 'unknown'
  ) {
    return true
  } else {
    return false
  }
}
</script>

<template>
  <div v-if="isLogin == true">
    <DataTable :data="tableData"></DataTable>
  </div>
  <div v-else>
    <Login @login="login"></Login>
  </div>
</template>

<style scoped></style>
