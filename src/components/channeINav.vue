<template>
    <van-tabs v-model:active="active" @click-tab="addlist(active)">
        <van-empty description="暂无数据" v-show="list.length == 0" />
        <van-tab @click-tab="addlist(item.id)" v-for="item in mydata" :title="item.name" :key="item.id">
            <div style="margin: 15px;" v-for="item in list">
                <h3 style="margin: auto;width: 85%; margin: 10px; ">{{ item.title }}</h3>
                <div class="noimg">
                    <img v-for="it in item.cover.images" :src="it" alt="">
                </div>
                <div
                    style="display: flex; justify-content: space-between; margin-top: 10px;margin-bottom: 15px; width: 85%; margin: auto; ">
                    <p style="color: #877e79">{{ item.aut_name }}</p>
                    <p style="color: #877e79 "> {{ item.pubdate }} </p>
                </div>
                <p style="border-bottom: 2px solid #d8d8d8;"></p>
            </div>
        </van-tab>
    </van-tabs>
</template>
<script setup lang='ts'>
import { ref, reactive } from 'vue';
let active = ref(0);


let mydata = ref([])
let list = ref([])
import axios from 'axios';
// 请求列表菜单数据
axios.get('http://geek.itheima.net/v1_0/channels').then(res => {
    mydata.value = res.data.data.channels
    console.log(mydata.value);
})
axios.get('http://geek.itheima.net/v1_0/articles?channel_id=1&timestamp=1636436800&with_top=1').then(res => {
    console.log(res.data.data.results);
    list.value = res.data.data.results
})
const addlist = (id: number) => {
    console.log(id);
    axios.get('http://geek.itheima.net/v1_0/articles?channel_id=' + id + '&timestamp=1636436800&with_top=1').then(res => {
        // console.log(res.data.data.results);
        list.value = res.data.data.results
    })
}
</script>
<style lang='scss' scoped>
.noimg {
    width: 80%;
    display: flex;

    img {
        width: 100px;
        height: 100px;
        margin: 0px 18px;
        border-radius: 15px;
    }
}
</style>