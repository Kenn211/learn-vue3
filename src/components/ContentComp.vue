<script lang="ts">
import { defineComponent, PropType, ref,reactive,toRaw } from 'vue';
import ListInfoComp from './ListInfoComp.vue';
import SearchComp from './SearchComp.vue';
import {Info} from '../interfaces/interfaces';
export default defineComponent({
    name: "ContentComp",
    components: {
    ListInfoComp,
    SearchComp
    },
    setup() {

        let listInfo:Info[] = reactive([
                { id: 1, title: "Build My To-do by VueJS", status: "Completed" },
                { id: 2, title: "Build a website for the final exam", status: "Has-due-date" },
                { id: 3, title: "Try hard, thăm ngàn,.....", status: "Active" },
                { id: 4, title: "Đi ngủ đã :))) Díu lắm rồi", status: "Completed" },
                { id: 5, title: "Bái Baiiiiii. Pà poiiiiiiiii.............", status: "Has-due-date" },
        ]);
        // let filter = ref('');

        function addInfo(data: any) {
            if (data.text.value == "" || data.text.value == null) {
                alert("Nhập vào thì mới thêm được");
            }
            else {
                const lenghtList: number = listInfo.length;
                listInfo.unshift({ id: lenghtList + 1, title: data.text.value, status: "Has-due-date" });
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

        function handleToActiveEvent(data: Info) {
            listInfo[(data.id) - 1].status = "Active"
        };

        function handleToCompletedEvent(data: Info) {
            listInfo[(data.id) - 1].status = "Completed"
        };

        function toHasDueDateEvent(data: Info) {
            listInfo[(data.id) - 1].status = "Has-due-date"
        };

        
        return{
            listInfo,addInfo,handleDeleteInfo,handleToActiveEvent,handleToCompletedEvent,toHasDueDateEvent
        }
    },
})
</script>

<template>
    <SearchComp @addInfo="addInfo"></SearchComp>
    <ListInfoComp :listInfo="listInfo" @deleteInfoEvent="handleDeleteInfo"
        @toActiveEvent="handleToActiveEvent" @toCompletedEvent="handleToCompletedEvent"
        @toHasDueDateEvent="toHasDueDateEvent"></ListInfoComp>
</template>