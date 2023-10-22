<template>
    <div id="body">
        <div class="login">
            <div class="box">
                <p class="table">登录</p>
                <br>
                <input type="text" placeholder="账号" id="user_name">
                <input type="password" placeholder="密码" id="user_pwd">
                <br>
                <a href="#" class="go" @click="login">启动!</a>
            </div>
        </div>
    </div>
    <!-- 作者：山羊の前端小窝 https://www.bilibili.com/read/cv18984273/ 出处：bilibili -->
</template>

<script setup>
import { onMounted } from 'vue';

const emit = defineEmits(['login'])
onMounted(() => {
    if (localStorage.getItem("user_name") != null && localStorage.getItem("user_pwd") != null && localStorage.getItem("user_name") != undefined && localStorage.getItem("user_pwd") != undefined) {
        document.querySelector("#user_name").value = localStorage.getItem("user_name")
        document.querySelector("#user_pwd").value = localStorage.getItem("user_pwd")
    }
})
function login() {
    const user_name = document.getElementById('user_name').value
    const user_pwd = document.getElementById('user_pwd').value
    localStorage.setItem("user_name", user_name)
    localStorage.setItem("user_pwd", user_pwd)
    emit("login")
}
</script>

<style scoped>
* {
    padding: 0;
    margin: 0;
    text-decoration: none;
}

#body {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background-image: url("./loginbg.jpg");
    background-size: cover;
}

.login {
    width: 370px;
    height: 300px;
    display: flex;
    justify-content: center;
    align-items: center;
    background: linear-gradient(to right bottom,
            rgba(255, 255, 255, .7),
            rgba(255, 255, 255, .5),
            rgba(255, 255, 255, .4));
    /* 使背景模糊化 */
    backdrop-filter: blur(10px);
    box-shadow: 0 0 20px #a29bfe;
    border-radius: 15px;
}

.table {
    font: 900 40px '';
    text-align: center;
    letter-spacing: 5px;
    color: #3d3d3d;
}

.box {
    overflow: hidden;
    display: flex;
    flex-direction: column;
}

.box input {
    width: 400px;
    height: 100%;
    margin-bottom: 20px;
    outline: none;
    border: 0;
    padding: 10px;
    background-color: transparent;
    border-bottom: 3px solid rgb(150, 150, 240);
    font: 900 16px '';
}

.go {
    text-align: center;
    display: block;
    height: 24px;
    padding: 12px;
    font: 900 20px '';
    border-radius: 10px;
    margin-top: 20px;
    color: #fff;
    letter-spacing: 3px;
    background-image: linear-gradient(to left,
            #fd79a8, #a29bf6);
}
</style>