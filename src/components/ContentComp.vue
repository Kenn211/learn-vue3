<script setup lang="ts">
import { reactive } from 'vue';
import ListInfoComp from './ListInfoComp.vue';
import SearchComp from './SearchComp.vue';
import {Info} from '../interfaces/interfaces';


let listInfo = reactive<Info[]>([
        { id: 1, title: "Build My To-do by VueJS", status: "Completed" },
        { id: 2, title: "Build a website for the final exam", status: "Has-due-date" },
        { id: 3, title: "Try hard, thăm ngàn,.....", status: "Active" },
        { id: 4, title: "Đi ngủ đã :))) Díu lắm rồi", status: "Completed" },
        { id: 5, title: "Bái Baiiiiii. Pà poiiiiiiiii.............", status: "Has-due-date" },
]);
// let filter = ref('');

function addInfo(data: string) {
    if (data == "" || data == null) {
        alert("Nhập vào thì mới thêm được");
    }
    else {
        const lenghtList: number = listInfo.length;
        listInfo.unshift({ id: lenghtList + 1, title: data, status: "Has-due-date" });
        console.log(listInfo);
    }
};

function handleDeleteInfo(data: Info): void {
    var indexDeleteInfo = -1;
    listInfo.forEach((i, index) => {
        if (i.id == data.id) {
            indexDeleteInfo = index;
            if (indexDeleteInfo != -1) {
                listInfo.splice(indexDeleteInfo, 1);
            }
        }
    });
};


function changeStatus(data: Info,status: string) {
    listInfo.map(item => {
        if(item.id == data.id){
                item.status = status;
        }
    });
}
</script>

<template>
    <SearchComp @addInfo="addInfo"></SearchComp>
    <ListInfoComp :listInfo="listInfo" @deleteInfo="handleDeleteInfo"
       @statusChange="changeStatus"></ListInfoComp>
</template>