<template>
    <div id="body">
        <div class="container">
            <table>
                <thead>
                    <tr>
                        <th>时间</th>
                        <th>里程</th>
                        <th>速度</th>
                        <th>有效</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="item in props.data">
                        <td>{{ item.runnerTime }}</td>
                        <td>{{ item.runnerMileage }}</td>
                        <td>{{ item.runnerSpeed.toString().slice(0,4) }}</td>
                        <td>{{ item.ok }}</td>
                    </tr>
                    <!-- <tr>
                        <td>1</td>
                        <td>2</td>
                        <td>3</td>
                        <td>4</td>
                    </tr> -->
                </tbody>
            </table>
        </div>
    </div>
</template>

<script setup>
import { onMounted } from 'vue';

const props = defineProps(['data'])
</script>

<style scoped>
* {
    /* 页面初始化 清除元素的内外边距 */
    padding: 0;
    margin: 0;
    /* 盒子模型 */
    box-sizing: border-box;
}

#body {
    /* 弹性布局 让页面元素垂直+水平居中 */
    display: flex;
    justify-content: center;
    align-items: center;
    background-image: url("./loginbg.jpg");
    /* 让页面高度占浏览器可视区域的高度 */
    height: 100vh;
    background-color: #4793e3;
    background-size: cover;
}

.container {
    /* 溢出隐藏 */
    overflow: hidden;
    /* 外边距 上下为0  左右为20px */
    margin: 0 5px;
    background-color: #fff;
    /* 盒子阴影 */
    box-shadow: 0 0 50px rgba(0, 0, 0, 0.5);
}

.container table {
    /* 让表格的边框合并在一起 */
    border-collapse: collapse;
}

/* 在做pc端 不注释掉看不到效果 */
.container table thead tr th {
    color: #fff;
    background-color: #4fc3a1;
}

/* 还是取单数 */
.container table thead tr th:nth-child(odd) {
    background-color: #324960;
}

.container table thead tr th,
.container table tbody tr td {
    text-align: center;
    /* 先不加 大屏就正常了 */
    padding: 20px 40px;
}

.container table tbody tr td {
    border: 1px solid rgb(200, 200, 200);
}

.container table tbody tr:nth-child(odd) {
    background-color: #f8f8f8;
}

/* 先做移动端 */
/* 媒体查询 当页面宽度小于765px时执行里面的代码 */
@media (max-width: 765px) {
    .container table {
        /* 让thead和tbody水平排列 */
        display: flex;
    }

    .container table thead tr {
        /* 让thead>tr下的每一个元素称为弹性项目*/
        display: flex;
        /* 改变主轴的方向 让弹性项目垂直排列*/
        flex-direction: column;
    }

    .container table tbody {
        display: flex;
        /* 溢出盒子时 自动适配滚动条 */
        overflow: auto;
    }

    .container table tbody tr {
        /* 同上 */
        display: flex;
        flex-direction: column;
    }

    .container table thead tr th,
    .container table tbody tr td {
        /* 文字左对齐 */
        text-align: left;
        width: 120px;
        padding: 10px;
        /* 先把所有边框清为0 再分别设置即可 */
        border: 0;
        border-bottom: 1px solid rgb(200, 200, 200);
        border-right: 1px solid rgb(200, 200, 200);
    }

    /* 去除每一行的最后一个单元格的下边框*/
    .container table thead tr th:last-child,
    .container table tbody tr td:last-child {
        border-bottom: 0;
    }

    .container table tbody tr td:nth-child(odd) {
        /* 让tbody下的每一行的单数的单元格的背景颜色为#f8f8f8 */
        background-color: #f8f8f8;
    }

    .container table tbody tr:nth-child(odd) {
        background-color: transparent;
    }
}
</style>