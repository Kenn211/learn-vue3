<script lang="ts">
import { defineComponent, PropType } from 'vue';
import ListInfoComp from './ListInfoComp.vue';
import SearchComp from './SearchComp.vue';
export default defineComponent({
    name: "ContentComp",
    components: {
    ListInfoComp,
    SearchComp
},
    data() {
        return {
            listInfo: [
                { id: 1, title: "Build My To-do by VueJS", status: "Completed" },
                { id: 2, title: "Build a website for the final exam", status: "Has-due-date" },
                { id: 3, title: "Try hard, thăm ngàn,.....", status: "Active" },
                { id: 4, title: "Đi ngủ đã :))) Díu lắm rồi", status: "Completed" },
                { id: 5, title: "Bái Baiiiiii. Pà poiiiiiiiii.............", status: "Has-due-date" },
            ],
            Filter: '',
        }
    },
    created() {
        this.listInfo
    },
    methods: {
        addInfo(data: any) {
            if (data.text.value == "" || data.text.value == null) {
                alert("Nhập vào thì mới thêm được");
            }
            else {
                const lenghtList: any = this.listInfo.length;
                this.listInfo.push({ id: lenghtList + 1, title: data.text.value, status: "Has-due-date" });
                console.log(this.listInfo)
            }
        },
        handleDeleteInfo(data: any): void {
            var indexDeleteInfo = -1;
            this.listInfo.forEach((i, index) => {
                if (i.id == data.id) {
                    indexDeleteInfo = index;
                    if (indexDeleteInfo != -1) {
                        this.listInfo.splice(indexDeleteInfo, 1);
                    }
                }
            });
        },
        handleToActiveEvent(data: any) {
            this.listInfo[(data.id) - 1].status = "Active"
        },
        handleToCompletedEvent(data: any) {
            this.listInfo[(data.id) - 1].status = "Completed"
        },
        toHasDueDateEvent(data: any) {
            this.listInfo[(data.id) - 1].status = "Has-due-date"
        },
    },
})
</script>

<template>
    <SearchComp @addInfo="addInfo"></SearchComp>
    <ListInfoComp v-bind:listInfo="listInfo" @deleteInfoEvent="handleDeleteInfo"
        @toActiveEvent="handleToActiveEvent" @toCompletedEvent="handleToCompletedEvent"
        @toHasDueDateEvent="toHasDueDateEvent"></ListInfoComp>
</template>